<%*
/*
Sposta tutte le note contenenti 'Archivio' o '#Archivio' in 'Archive/'
✅ Forza l'eliminazione della nota corrente "Untitled"
✅ Ignora specificamente 'Grafici di utilizzo.md'
✅ Evita conflitti di nome nella cartella Archive
*/

// --- 1. AUTODISTRUZIONE NOTA TEMPLATE ---
const currentFile = tp.config.target_file;
// Chiudiamo la vista per sbloccare il file Untitled
app.workspace.getLeaf().setViewState({ type: "empty" });

// Eliminiamo la nota generata con un piccolo delay
setTimeout(() => {
    app.vault.trash(currentFile, true);
}, 100);

// --- 2. CONFIGURAZIONE ---
const allFiles = app.vault.getMarkdownFiles();
const tagRegex = /#?\bArchivio\b/i;                 
const destFolder = "Archive";                       
const excludeFolders = ["Templates", "Archive", "Bookshelf"];
const ignoreSpecificFiles = ["Grafici di utilizzo.md"]; 
const dryRun = false;                               

let toMove = [];

// --- 3. LOGICA DI RICERCA ---
for (const file of allFiles) {
  // Ignora la nota che stiamo eliminando ora
  if (file.path === currentFile.path) continue;

  // Ignora cartelle escluse
  if (excludeFolders.some(folder => file.path.startsWith(folder + "/"))) continue;
  
  // Ignora il file permanente
  if (ignoreSpecificFiles.includes(file.name)) continue;

  const content = await app.vault.read(file);
  if (tagRegex.test(content)) {
    toMove.push(file);
    console.log("📌 Trovato per archivio:", file.path);
  }
}

// Crea la cartella Archive se manca
try {
  if (!app.vault.getAbstractFileByPath(destFolder)) {
    await app.vault.createFolder(destFolder);
  }
} catch (e) {}

// --- 4. SPOSTAMENTO ---
if (toMove.length === 0) {
  new Notice("✅ Nessun file da archiviare");
} else {
  for (const f of toMove) {
    let destPath = `${destFolder}/${f.name}`;

    // Evita conflitti di nome
    let counter = 1;
    while (app.vault.getAbstractFileByPath(destPath)) {
      const name = f.name.replace(/\.md$/, `_${counter}.md`);
      destPath = `${destFolder}/${name}`;
      counter++;
    }

    try {
      if (!dryRun) {
        await app.fileManager.renameFile(f, destPath);
        await new Promise(resolve => setTimeout(resolve, 50));
      }
    } catch (err) {
      console.error(`❌ Errore spostando ${f.path}: ${err.message}`);
    }
  }

  new Notice(`📦 Archiviati ${toMove.length} file in '${destFolder}'`);
}
%>