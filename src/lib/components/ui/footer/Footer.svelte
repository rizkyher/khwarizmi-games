<script lang="ts">
  import { Github, Twitter, Mail, Heart, Terminal } from "@lucide/svelte";
</script>

<footer class="relative mt-32 pt-24 bg-[#283618] text-[#fefae0] overflow-hidden border-t-8 border-[#606c38]">
  <div
    class="absolute top-0 left-0 w-full h-8 bg-[#606c38]/30"
    style="clip-path: polygon(0% 100%, 3% 20%, 6% 80%, 10% 30%, 15% 90%, 20% 40%, 25% 85%, 30% 20%, 35% 95%, 42% 35%, 50% 80%, 58% 25%, 65% 90%, 72% 40%, 80% 85%, 88% 20%, 95% 90%, 100% 100%);"
  ></div>

  <div class="absolute inset-0 pointer-events-none">
    {#each Array(8) as _, i}
      <div
        class="firefly absolute size-1.5 bg-[#dda15e] rounded-full"
        style="
          left: {Math.random() * 100}%; 
          top: {Math.random() * 100}%; 
          animation-delay: {i * 2}s;
          box-shadow: 0 0 10px 2px #dda15e;
        "
      ></div>
    {/each}
  </div>

  <div class="container mx-auto px-6 max-w-6xl relative z-10 pb-12">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-16 mb-20">
      <div class="space-y-6">
        <div class="flex items-center gap-3 group cursor-default">
          <div class="size-10 bg-[#dda15e] border-2 border-white flex items-center justify-center rotate-3 group-hover:rotate-0 transition-transform shadow-[4px_4px_0px_#606c38]">
            <span class="text-lg">🏡</span>
          </div>
          <h3 class="font-pixel text-4xl tracking-tighter uppercase group-hover:text-[#dda15e] transition-colors">
            GHP_Studio<span class="animate-pulse">.</span>exe
          </h3>
        </div>
        <p class="font-pixel text-xl text-[#fefae0]/70 leading-snug">Crafting digital worlds with the warmth of hand-drawn dreams and the charm of pixel craftsmanship.</p>
      </div>

      <div class="font-pixel">
        <h4 class="text-[#dda15e] text-2xl uppercase mb-8 tracking-widest flex items-center gap-2">
          <Terminal size={18} /> // Quick_Travel
        </h4>
        <ul class="space-y-4 text-2xl">
          {#each ["HOME", "LIBRARY", "ARCHITECTS"] as link}
            <li>
              <a href="#{link.toLowerCase()}" class="flex items-center gap-2 hover:text-[#dda15e] transition-all group w-fit">
                <span class="opacity-0 group-hover:opacity-100 transition-opacity">→</span>
                <span class="group-hover:translate-x-1 transition-transform">{link}</span>
              </a>
            </li>
          {/each}
        </ul>
      </div>

      <div class="font-pixel">
        <h4 class="text-[#dda15e] text-2xl uppercase mb-8 tracking-widest">// Connection</h4>
        <div class="flex gap-4 mb-8">
          {#each [{ icon: Github, url: "https://github." }, { icon: Twitter, url: "https://twitter." }, { icon: Mail, url: "mailto:" }] as social}
            <a
              href={social.url}
              target="_blank"
              class="size-14 bg-[#606c38]/40 border-2 border-[#fefae0]/20 flex items-center justify-center hover:bg-[#dda15e] hover:text-[#283618] hover:-translate-y-2 transition-all shadow-[4px_4px_0px_#1a1a1a]"
            >
              <social.icon size={24} />
            </a>
          {/each}
        </div>
        <div class="flex items-center gap-2 bg-black/20 p-3 border-l-4 border-[#dda15e] w-fit">
          <div class="size-2 bg-[#dda15e] rounded-full animate-ping"></div>
          <p class="text-xs uppercase tracking-[0.2em] opacity-60">Status: System_Optimal</p>
        </div>
      </div>
    </div>

    <div class="pt-10 border-t border-[#fefae0]/10 flex flex-col md:flex-row justify-between items-center gap-6 font-pixel text-xl text-[#fefae0]/40 uppercase tracking-tight">
      <p>© 2026 GHP_Studio - <span class="text-[#dda15e]/50">All Bytes Reserved</span></p>

      <div class="flex items-center gap-2 bg-[#fefae0]/5 px-4 py-1 rounded-full border border-white/5">
        Made with <Heart size={16} class="text-[#e76f51] fill-[#e76f51] animate-pulse" />
        <span>in the pixel meadow</span>
      </div>
    </div>
  </div>

  <div class="absolute -bottom-20 -right-20 size-64 bg-[#dda15e]/5 rounded-full blur-[100px]"></div>
</footer>

<style>
  /* Menggunakan font yang sudah didefinisikan secara global sebelumnya */
  .font-pixel {
    font-family: "VT323", monospace;
  }

  /* Firefly Animation */
  @keyframes firefly-move {
    0%,
    100% {
      transform: translate(0, 0) scale(1);
      opacity: 0.2;
    }
    50% {
      transform: translate(50px, -50px) scale(1.2);
      opacity: 0.8;
    }
    75% {
      transform: translate(-20px, -80px) scale(0.8);
      opacity: 0.4;
    }
  }

  .firefly {
    animation: firefly-move 10s ease-in-out infinite;
  }

  /* Footer noise texture */
  footer::after {
    content: "";
    position: absolute;
    inset: 0;
    background-image: url("https://www.transparenttextures.com/patterns/p6.png");
    opacity: 0.05;
    pointer-events: none;
  }
</style>
