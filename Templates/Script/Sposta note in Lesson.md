<%*
/*
Sposta tutte le note contenenti 'TO-DO' o '#TO-DO' in 'Lesson/'
✅ Forza l'eliminazione della nota corrente "Untitled" con ritardo
✅ Ignora 'Grafici di utilizzo.md'
*/

// --- 1. AUTODISTRUZIONE NOTA TEMPLATE (Fix per Untitled) ---
const currentFile = tp.config.target_file;
// Chiudiamo il file attivo prima di eliminarlo per evitare blocchi
app.workspace.getLeaf().setViewState({ type: "empty" });

// Eliminiamo con un brevissimo ritardo
setTimeout(() => {
    app.vault.trash(currentFile, true);
}, 100);

// --- 2. CONFIGURAZIONE ---
const allFiles = app.vault.getMarkdownFiles();          
const tagRegex = /#?\bTO-DO\b/i;                        
const destFolder = "Lesson";                            
const excludeFolders = ["Templates", "Lesson", "Bookshelf"];
const ignoreSpecificFiles = ["Grafici di utilizzo.md"]; 
const dryRun = false;                                   

let toMove = [];

// --- 3. LOGICA DI RICERCA ---
for (const file of allFiles) {
  // Evitiamo di processare la nota che stiamo cancellando
  if (file.path === currentFile.path) continue;

  // Ignora se il file è in una cartella esclusa
  if (excludeFolders.some(folder => file.path.startsWith(folder + "/"))) continue;
  
  // Ignora specificamente il file "Grafici di utilizzo.md"
  if (ignoreSpecificFiles.includes(file.name)) continue;

  const content = await app.vault.read(file);
  if (tagRegex.test(content)) {
    toMove.push(file);
  }
}

// Crea la cartella se manca
try {
  if (!app.vault.getAbstractFileByPath(destFolder)) {
    await app.vault.createFolder(destFolder);
  }
} catch (e) {}

// --- 4. SPOSTAMENTO ---
if (toMove.length === 0) {
  new Notice("✅ Nessun file da spostare");
} else {
  for (const f of toMove) {
    let destPath = `${destFolder}/${f.name}`;
    let counter = 1;
    while (app.vault.getAbstractFileByPath(destPath)) {
      const name = f.name.replace(/\.md$/, `_${counter}.md`);
      destPath = `${destFolder}/${name}`;
      counter++;
    }

    try {
      if (!dryRun) {
        await app.fileManager.renameFile(f, destPath);
        await new Promise(r => setTimeout(r, 50));
      }
    } catch (err) {
      console.error(`❌ Errore: ${err.message}`);
    }
  }
  new Notice(`📦 Spostati ${toMove.length} file in '${destFolder}'`);
}
%>