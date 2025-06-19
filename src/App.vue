<!-- src/App.vue -->
<template>
  <div class="bg-gray-100 min-h-screen">
    <!-- Top Banner -->
    <div class="bg-black h-10 shadow-lg flex items-center">
      <div class="w-full px-4 flex items-center justify-between">
        <h1 class="text-lg font-bold text-white">
          <span class="bg-gradient-to-r from-yellow-200 to-pink-200 bg-clip-text text-transparent drop-shadow-lg">
            EvalMSA
          </span>
        </h1>
        <p class="text-gray-300 text-xs font-medium">Multiple Sequence Alignment Evaluation Portal</p>
      </div>
    </div>

    <!-- Main Content -->
    <div class="flex min-h-screen">
      <div class="w-full flex">
        <!-- Left Pane - Logo and Description -->
        <div class="w-1/4 bg-gradient-to-br from-blue-50 via-indigo-50 to-purple-50 p-6 flex flex-col justify-start">
          <!-- Protein Alignment Logo -->
          <div class="text-center mb-6">
            <div class="font-mono text-xs space-y-px inline-block bg-gradient-to-r from-slate-100 to-slate-50 p-3 rounded-lg border shadow-sm">
              <div class="flex">
                <span class="bg-red-100 text-red-700 px-1">M</span>
                <span class="bg-blue-100 text-blue-700 px-1">K</span>
                <span class="bg-green-100 text-green-700 px-1">V</span>
                <span class="bg-yellow-100 text-yellow-700 px-1">L</span>
                <span class="bg-purple-100 text-purple-700 px-1">S</span>
                <span class="bg-pink-100 text-pink-700 px-1">A</span>
                <span class="bg-indigo-100 text-indigo-700 px-1">D</span>
                <span class="bg-cyan-100 text-cyan-700 px-1">F</span>
                <span class="bg-orange-100 text-orange-700 px-1">G</span>
              </div>
              <div class="flex">
                <span class="bg-red-100 text-red-700 px-1">M</span>
                <span class="bg-blue-100 text-blue-700 px-1">K</span>
                <span class="bg-gray-100 text-gray-500 px-1">-</span>
                <span class="bg-yellow-100 text-yellow-700 px-1">L</span>
                <span class="bg-purple-100 text-purple-700 px-1">S</span>
                <span class="bg-pink-100 text-pink-700 px-1">A</span>
                <span class="bg-indigo-100 text-indigo-700 px-1">D</span>
                <span class="bg-cyan-100 text-cyan-700 px-1">F</span>
                <span class="bg-orange-100 text-orange-700 px-1">G</span>
              </div>
              <div class="flex">
                <span class="bg-red-100 text-red-700 px-1">M</span>
                <span class="bg-blue-100 text-blue-700 px-1">K</span>
                <span class="bg-green-100 text-green-700 px-1">V</span>
                <span class="bg-gray-100 text-gray-500 px-1">-</span>
                <span class="bg-purple-100 text-purple-700 px-1">S</span>
                <span class="bg-pink-100 text-pink-700 px-1">A</span>
                <span class="bg-indigo-100 text-indigo-700 px-1">D</span>
                <span class="bg-cyan-100 text-cyan-700 px-1">F</span>
                <span class="bg-orange-100 text-orange-700 px-1">G</span>
              </div>
            </div>
          </div>

          <!-- Portal Description -->
          <div class="text-center">
            <div class="bg-white/70 p-4 rounded-xl border border-blue-100 shadow-sm backdrop-blur-sm">
              <div class="flex items-center justify-center mb-3">
                <div class="w-10 h-10 bg-gradient-to-br from-blue-500 to-indigo-600 rounded-full flex items-center justify-center">
                  <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
                  </svg>
                </div>
              </div>
              <h2 class="text-lg font-bold text-gray-800 mb-3">Protein Alignment Portal</h2>
              <p class="text-gray-600 leading-relaxed mb-4 text-sm">
                Compare and evaluate multiple sequence alignment algorithms for your protein sequences. 
                Upload your data, select from industry-standard alignment tools, and receive comprehensive 
                results delivered directly to your inbox.
              </p>
              <div class="flex flex-col space-y-2 text-xs text-gray-600">
                <span class="flex items-center justify-center">
                  <div class="w-2 h-2 bg-green-400 rounded-full mr-2"></div>
                  Fast Processing
                </span>
                <span class="flex items-center justify-center">
                  <div class="w-2 h-2 bg-blue-400 rounded-full mr-2"></div>
                  Multiple Tools
                </span>
                <span class="flex items-center justify-center">
                  <div class="w-2 h-2 bg-purple-400 rounded-full mr-2"></div>
                  Email Results
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- Right Pane - Form -->
        <div class="w-3/4 bg-white p-8 flex-1">
          <h1 class="text-2xl font-bold mb-6 text-center">Alignment Program Selection</h1>
          <form @submit.prevent="submitForm" class="space-y-4">
            <div>
              <label class="block mb-2 text-lg font-semibold">Sequence Input:</label>
              <textarea
                v-model="sequence"
                rows="8"
                class="w-full px-4 py-3 text-base border-2 border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent resize-y min-h-[200px]"
                placeholder="Paste or type your sequence here..."
                required
              ></textarea>
            </div>

            <div>
              <label class="block mb-2 text-lg font-semibold">Or Upload Sequence File:</label>
              <input
                type="file"
                @change="handleFileUpload"
                accept=".txt,.fasta,.seq,.gb"
                class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg file:mr-4 file:rounded-md file:border-0 file:bg-blue-50 file:px-4 file:py-2 file:text-blue-700 hover:file:bg-blue-100 file:font-semibold"
              />
            </div>

            <div>
              <p class="mb-3 text-lg font-semibold">Select Alignment Programs:</p>
              <div class="grid grid-cols-2 gap-3">
                <label
                  v-for="[label, value] in Object.entries(options)"
                  :key="value"
                  class="flex items-center bg-gray-50 p-3 rounded-lg border border-gray-200 hover:bg-blue-50 transition duration-200"
                >
                 <input
                    type="checkbox"
                    :value="value"
                    v-model="selectedPrograms"
                    class="w-5 h-5 text-blue-600 focus:ring-blue-500 border-gray-300 rounded mr-3 flex-shrink-0"
                  />
                <span class="text-base font-medium">{{ label }}</span>
             </label>
              </div>
            </div>

            <div>
              <label class="block mb-1 font-medium">Email Address:</label>
              <input
                type="email"
                v-model="email"
                class="w-full px-3 py-2 border rounded-md"
                required
              />
            </div>

            <button
              type="submit"
              class="w-full bg-blue-500 text-white py-2 rounded-md hover:bg-blue-600 transition duration-300"
            >
              Submit
            </button>

            <p v-if="error" class="text-red-500 mt-4">{{ error }}</p>
            <p v-if="response" class="text-green-600 mt-4">✅ Evaluation complete. Check results in your Email!</p>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sequence: '',
      email: '',
      selectedPrograms: [],
      options: {
            'Muscle': 'muscle',
            'MAFFT': 'mafft',
            //'DIALIGN': 'dalign',
            'T-Coffee': 't_coffee',
            'Probcons':'probcons',
            'Kalign':'kalign',
            'Clustalo':'clustalo',
            'Prank': 'prank'
          },
      error: '',
      response: null,
    };
  },
  methods: {
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = (e) => {
        this.sequence = e.target.result;
      };
      reader.readAsText(file);
    },
    async submitForm() {
      this.error = '';
      this.response = null;

      if (!this.sequence || this.selectedPrograms.length === 0 || !this.email) {
        this.error = 'All fields are required and at least one program must be selected.';
        return;
      }

      try {
        const res = await fetch('http://localhost:8000/evaluate', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            sequence: this.sequence,
            email: this.email,
            programs: this.selectedPrograms,
          }),
        });

        if (!res.ok) throw new Error('Evaluation failed');

        this.response = await res.json();
      } catch (err) {
        this.error = err.message || 'Submission failed';
      }
    },
  },
};
</script>

<style scoped>
/*textarea:invalid,
input:invalid {
  border-color: red;
}*/
</style>