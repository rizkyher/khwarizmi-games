<script lang="ts">
  import { Github, Twitter, Mail, Heart } from "@lucide/svelte";
</script>

<footer class="relative mt-32 pt-20 bg-[#283618] text-[#fefae0] overflow-hidden">
  <div class="absolute top-0 left-0 w-full h-12 bg-[#606c38] -translate-y-full">
    <div class="absolute bottom-0 w-full h-6 bg-[#283618] opacity-30" style="clip-path: polygon(0% 100%, 5% 20%, 10% 80%, 15% 40%, 22% 90%, 30% 30%, 38% 85%, 45% 15%, 55% 95%, 65% 25%, 75% 80%, 85% 35%, 92% 90%, 100% 100%);"></div>
  </div>

  <div class="container mx-auto px-6 max-w-6xl relative z-10 pb-12">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-16 mb-20">
      <div class="space-y-6">
        <div class="flex items-center gap-3">
          <div class="size-8 bg-[#dda15e] border-2 border-white flex items-center justify-center">
            <span class="text-sm">🏠</span>
          </div>
          <h3 class="font-['VT323'] text-3xl tracking-tighter uppercase">GHP_Studio.exe</h3>
        </div>
        <p class="font-['VT323'] text-xl text-[#fefae0]/60 leading-relaxed">Crafting digital worlds with the warmth of hand-drawn dreams and the charm of pixels.</p>
      </div>

      <div class="font-['VT323']">
        <h4 class="text-[#dda15e] text-2xl uppercase mb-6 tracking-widest">// Quick_Travel</h4>
        <ul class="space-y-3 text-xl">
          <li><a href="#hero" class="hover:text-[#dda15e] transition-colors hover:pl-2">-> HOME</a></li>
          <li><a href="#archive" class="hover:text-[#dda15e] transition-colors hover:pl-2">-> LIBRARY</a></li>
          <li><a href="#mechanics" class="hover:text-[#dda15e] transition-colors hover:pl-2">-> ARCHITECTS</a></li>
        </ul>
      </div>

      <div class="font-['VT323']">
        <h4 class="text-[#dda15e] text-2xl uppercase mb-6 tracking-widest">// Connection</h4>
        <div class="flex gap-4 mb-8">
          <a href="/" class="size-12 bg-[#606c38] border-2 border-[#fefae0]/20 flex items-center justify-center hover:bg-[#dda15e] hover:text-[#283618] transition-all">
            <Github size={20} />
          </a>
          <a href="/" class="size-12 bg-[#606c38] border-2 border-[#fefae0]/20 flex items-center justify-center hover:bg-[#dda15e] hover:text-[#283618] transition-all">
            <Twitter size={20} />
          </a>
          <a href="/" class="size-12 bg-[#606c38] border-2 border-[#fefae0]/20 flex items-center justify-center hover:bg-[#dda15e] hover:text-[#283618] transition-all">
            <Mail size={20} />
          </a>
        </div>
        <p class="text-xs opacity-40 uppercase tracking-[0.2em]">Status: System_Optimal</p>
      </div>
    </div>

    <div class="pt-8 border-t border-[#fefae0]/10 flex flex-col md:flex-row justify-between items-center gap-4 font-['VT323'] text-lg text-[#fefae0]/40 uppercase">
      <p>© 2026 GHP_Studio - All Bytes Reserved</p>
      <div class="flex items-center gap-2">
        Made with <Heart size={14} class="text-[#e76f51] fill-[#e76f51]" /> in the pixel meadow
      </div>
    </div>
  </div>

  <div class="absolute bottom-20 left-1/4 size-1 bg-[#dda15e] animate-pulse rounded-full shadow-[0_0_10px_#dda15e]"></div>
  <div class="absolute bottom-40 right-1/3 size-1 bg-[#dda15e] animate-pulse rounded-full shadow-[0_0_10px_#dda15e]" style="animation-delay: 1s"></div>
</footer>
