# Testing
## Penjelasan Teknis
1. localStorage (Penyimpanan Data)
   '''javascript
   function saveToStorage() {
    localStorage.setItem("tugas", JSON.stringify(tasks));
}

3. Validasi Form
   '''javascript
   document.getElementById("formTugas").addEventListener("submit", function(e) {
    e.preventDefault();
    
    const nama = document.getElementById("namaTugas").value.trim();
    const matkul = document.getElementById("mataKuliah").value.trim();
    const deadline = document.getElementById("deadline").value;
    
    // Validasi field tidak boleh kosong
    if (!nama || !matkul || !deadline) {
        alert("Nama, mata kuliah, dan deadline harus diisi!");
        return;
    }
    
    // Validasi deadline tidak di masa lalu
    const today = new Date();
    today.setHours(0, 0, 0, 0);
    const taskDate = new Date(deadline);
    
    if (taskDate < today) {
        alert("Deadline tidak boleh di masa lalu!");
        return;
    }
    
    // Jika valid, tambahkan tugas...

});

3. Filter dan pencarian real-time
   '''javascript
   function displayTasks() {
    const searchVal = document.getElementById("cari").value.toLowerCase();
    const filterVal = document.getElementById("filterStatus").value;
    
    let filteredTasks = tasks.filter(function(task) {
        const matchSearch = task.nama.toLowerCase().includes(searchVal) || 
                          task.matkul.toLowerCase().includes(searchVal);
        const matchStatus = filterVal === "semua" || 
                          (filterVal === "selesai" && task.selesai) || 
                          (filterVal === "belum" && !task.selesai);
        return matchSearch && matchStatus;
    });
}

// Event listener untuk real-time
document.getElementById("filterStatus").addEventListener("change", displayTasks);
document.getElementById("cari").addEventListener("input", displayTasks);

4. Update statistik
   '''javascript
   function updateStats() {
    const total = tasks.length;
    const done = tasks.filter(t => t.selesai).length;
    const notDone = total - done;
    
    document.getElementById("totalTugas").textContent = total;
    document.getElementById("tugasSelesai").textContent = done;
    document.getElementById("tugasBelum").textContent = notDone;
}
