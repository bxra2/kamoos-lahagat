<script lang="ts">
  import "../app.css";
  let text = "";
  let isValidArabic = true;
  const imageUrl = "./calligraphy-dark.png";

  // Arabic regex to allow Arabic characters, Arabic numerals, and spaces only
  const arabicRegex = /^[\u0600-\u06FF\s0-9]+$/;

  function validateArabicInput(event: KeyboardEvent) {
    const char = event.key; // Get the character typed by the user

    // Allow backspace, delete, arrow keys and other special keys
    if (event.key === "Backspace" || event.key === "Delete" || event.key === "ArrowLeft" || event.key === "ArrowRight" || event.key === "ArrowUp" || event.key === "ArrowDown") {
      return; // Allow backspace and arrow keys
    }

    // Check if the typed character is not Arabic (including Arabic numerals)
    if (!char.match(/[\u0600-\u06FF\s0-9]/)) {
      event.preventDefault(); // Prevent the key from being entered
      isValidArabic = false; // Optionally, show feedback about invalid input
    } else {
      isValidArabic = true;
    }
  }
</script>

<svelte:head>
  <title>Home</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
  <div style="background-image: url('{imageUrl}')" class="background h-screen flex flex-col justify-center">
    <div class="bg-[#F1F1F1] shadow-xl w-2/3 rounded-lg p-6 max-w-6xl mx-auto">
      <div class="">
        <div class="text-center">
          <h1 class="text-4xl font-extrabold text-[#483628] sm:text-5xl md:text-6xl">مترجم اللهجات</h1>
          <p class="mt-4 max-w-md mx-auto text-base text-gray-500 sm:text-lg md:mt-5 md:text-xl md:max-w-3xl">الترجمة الاحترافية من وإلى العديد من اللهجات بدقة وجودة</p>
        </div>
        <div class="grid grid-rows-[20px_1fr_20px] items-start justify-items-center p-2 pb-2 gap-4 sm:p-6 font-[family-name:var(--font-geist-sans)]">
          <div class="flex flex-col gap-8 row-start-2 items-center sm:items-start w-full">
            <form
              class="w-full"
              action="javascript:throw new Error('A React form was unexpectedly submitted. If you called form.submit() manually, consider using form.requestSubmit() instead. If you\'re trying to use event.stopPropagation() in a submit event handler, consider also calling event.preventDefault().')"
            >
              <div class="flex flex-row gap-4">
                <div class="container flex flex-col">
                  <div class="justify-between flex">
                    <select name="languageTo" class="rounded-md bg-background px-3 py-2 focus:border-[#f5ebd2] mb-2 w-fit">
                      <option value="en">English</option>
                      <option value="es">Spanish</option>
                      <option value="fr">French</option>
                    </select>
                  </div>
                  <textarea rows="5" placeholder="سيظهر النص المترجم هنا" class="rounded-md p-4 borderrounded-md cursor-default resize-none" readonly dir="rtl" />
                </div>
                <div class="container flex flex-col">
                  <select name="languageFrom" class="rounded-md bg-background px-3 py-2 focus:border-[#f5ebd2] mb-2 w-fit">
                    <option value="en" selected="">English</option>
                    <option value="es">Spanish</option>
                    <option value="fr">French</option>
                  </select>
                  <textarea
                    bind:value={text}
                    rows="5"
                    placeholder="أدخل النص للترجمة"
                    class="borderrounded-md rounded-md p-4 resize-none {isValidArabic ? '' : 'border-red-500'}"
                    name="text"
                    required
                    on:keydown={validateArabicInput}
                    dir="rtl"
                  />
                </div>
              </div>
              <div class="flex flex-row items-center gap-2 h-16">
                <button type="submit" class="p-2 rounded-md bg-[#483628] text-white">ترجم </button>
                <div class="flex items-center p-4">
                  <!-- <button
                                          type="button"
                                          class="w-12 h-12 rounded-full border flex items-center justify-center"
                                      >
                                          <svg
                                              xmlns="http://www.w3.org/2000/svg"
                                              width="24"
                                              height="24"
                                              viewBox="0 0 24 24"
                                              fill="none"
                                              stroke="currentColor"
                                              stroke-width="2"
                                              stroke-linecap="round"
                                              stroke-linejoin="round"
                                              class="lucide lucide-mic w-4 h-4"
                                              ><path
                                                  d="M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3Z"
                                              ></path><path
                                                  d="M19 10v2a7 7 0 0 1-14 0v-2"
                                              ></path><line
                                                  x1="12"
                                                  x2="12"
                                                  y1="19"
                                                  y2="22"
                                              ></line></svg
                                          ></button
                                      > -->
                  <input type="hidden" aria-label="Recorded audio" name="audio" value="" />
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .background {
    width: 100%;
    background-size: cover;
    background-position: center;
  }
</style>
