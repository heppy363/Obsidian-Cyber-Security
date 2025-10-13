<%*
/*
Sposta tutte le note contenenti 'Completed' o '#Completed' in 'Processed/'
✅ Funziona anche se c’è una sola nota
✅ Evita cartelle Templates e Bookshelf
✅ Non crea nuove note
*/

const active = app.workspace.getActiveFile();         
const allFiles = app.vault.getMarkdownFiles();        
const tagRegex = /#?\bCompleted\b/i;                         
const destFolder = "Processed";                          
const excludeFolders = ["Templates", "Bookshelf", "Processed"];       
const dryRun = false;                                 

let toMove = [];

// Trova i file da spostare
for (const file of allFiles) {
  if (active && file.path === active.path) continue;
  if (excludeFolders.some(folder => file.path.split("/")[0] === folder)) continue;

  const content = await app.vault.read(file);
  if (tagRegex.test(content)) {
    toMove.push(file);
    console.log("Trovato tag in:", file.path);
  }
}

// Crea la cartella se manca
try {
  await app.vault.createFolder(destFolder);
} catch (e) {}

// Sposta davvero
if (toMove.length === 0) {
  new Notice("✅ Nessun file da spostare (nessun 'Completed' trovato)");
} else {
  for (const f of toMove) {
    let destPath = `${destFolder}/${f.name}`;
    
    // evita conflitti se il file esiste già
    let counter = 1;
    while (app.vault.getAbstractFileByPath(destPath)) {
      const name = f.name.replace(/\.md$/, `_${counter}.md`);
      destPath = `${destFolder}/${name}`;
      counter++;
    }

    try {
      if (!dryRun) {
        await app.fileManager.renameFile(f, destPath);
        // 👇 Fix per il caso con un solo file
        await new Promise(resolve => setTimeout(resolve, 100));
      }
      console.log(`✅ Spostato: ${f.path} → ${destPath}`);
    } catch (err) {
      console.error(`❌ Errore spostando ${f.path}: ${err.message}`);
    }
  }

  new Notice(`📦 Spostati ${toMove.length} file in '${destFolder}'`);
}
%>
