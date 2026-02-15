<%*
/*
Sposta tutte le note contenenti 'Completed' o '#Completed' in 'Processed/'
✅ Autodistrugge la nota temporanea (Untitled)
✅ Ignora specificamente 'Grafici di utilizzo.md'
✅ Evita duplicati e conflitti di nome
*/

// --- 1. PULIZIA AMBIENTE (Autodistruzione nota creata) ---
const currentFile = tp.config.target_file;
// Svuota la vista attiva per sbloccare il file
app.workspace.getLeaf().setViewState({ type: "empty" });

// Elimina il file "Untitled" con un piccolo delay per sicurezza
setTimeout(() => {
    app.vault.trash(currentFile, true);
}, 100);

// --- 2. CONFIGURAZIONE ---
const allFiles = app.vault.getMarkdownFiles();          
const tagRegex = /#?\bCompleted\b/i;                        
const destFolder = "Processed";                            
const excludeFolders = ["Templates", "Bookshelf", "Processed"];
const ignoreSpecificFiles = ["Grafici di utilizzo.md"]; 
const dryRun = false;                                   

let toMove = [];

// --- 3. RICERCA FILE ---
for (const file of allFiles) {
  // Ignora la nota che stiamo cancellando
  if (file.path === currentFile.path) continue;

  // Ignora se il file è in una cartella esclusa
  if (excludeFolders.some(folder => file.path.startsWith(folder + "/"))) continue;
  
  // Ignora il file permanente indicato
  if (ignoreSpecificFiles.includes(file.name)) continue;

  const content = await app.vault.read(file);
  if (tagRegex.test(content)) {
    toMove.push(file);
  }
}

// Crea la cartella Processed se manca
try {
  if (!app.vault.getAbstractFileByPath(destFolder)) {
    await app.vault.createFolder(destFolder);
  }
} catch (e) {}

// --- 4. ESECUZIONE SPOSTAMENTO ---
if (toMove.length === 0) {
  new Notice("✅ Nessun file da spostare (nessun 'Completed' trovato)");
} else {
  for (const f of toMove) {
    let destPath = `${destFolder}/${f.name}`;
    
    // Gestione conflitti di nome (evita sovrascritture)
    let counter = 1;
    while (app.vault.getAbstractFileByPath(destPath)) {
      const name = f.name.replace(/\.md$/, `_${counter}.md`);
      destPath = `${destFolder}/${name}`;
      counter++;
    }

    try {
      if (!dryRun) {
        await app.fileManager.renameFile(f, destPath);
        // Pausa per stabilità del file system
        await new Promise(resolve => setTimeout(resolve, 50));
      }
      console.log(`✅ Spostato: ${f.path} → ${destPath}`);
    } catch (err) {
      console.error(`❌ Errore spostando ${f.path}: ${err.message}`);
    }
  }

  new Notice(`📦 Archiviate ${toMove.length} note in '${destFolder}'`);
}
%>