<script lang="ts">
  import Header from "./lib/Header.svelte";
  import { scrollTo, scrollRef } from 'svelte-scrolling'
  import ScrollLink from "./lib/scrollLink.svelte";

  import Scroller from "@sveltejs/svelte-scroller";
  import { setGlobalOptions } from 'svelte-scrolling'
  import { cubicInOut } from 'svelte/easing';
  import Text from "./lib/Text.svelte";
  import Subheader from "./lib/Subheader.svelte";
  import roomCW from './assets/2roomCW.png';
  import profilePic from './assets/linkedinprofile.png'
  import PopupLink from "./lib/popupLink.svelte";
    import ScrollLinkMobile from "./lib/scrollLinkMobile.svelte";

  setGlobalOptions({
      duration: 800,
      offset: 0,
      easing: cubicInOut,
      onStart: () => {isAutoScrolling = true},
      onDone: () => {isAutoScrolling = false}
  });

  let isAutoScrolling = false; 
  let tempIndex = 0;

  let index = 0;
  let top = 0;
  let threshold = 0.5;
  let bottom = 1;
  let innerWidth = 0;
  $: isMobile = innerWidth <= 750

  let topbarHeight = 100;
</script>

<svelte:window bind:innerWidth />

<main class="min-h-screen min-w-screen flex overflow-x-hidden">

  {#if !isMobile}
  <!-- Sidebar -->
  <div class="bg-cyan-950 min-h-full w-[260px] fixed z-[10] overscroll-y-none shadow-black text-blue-50">

    <div class="flex flex-col items-center">
      
      <div class="w-full flex flex-col items-center gap-2 bg-cyan-900 border-b border-b-blue-50 py-8 pb-6">
        <div class="h-[160px] w-[160px] bg-cyan-950 rounded-full">
          <!-- svelte-ignore a11y-img-redundant-alt -->
          <img class="rounded-full" src={profilePic} alt="Profile picture, Robin Salminen" >
        </div>
        <h2 class="font-medium font-mono">Robin Salminen</h2>
      </div>

      <div class="flex flex-col w-full items-end pt-8 gap-1 text-[17px] font-medium">
        <ScrollLink str={"About me"} refStr={'about'} bind:index={index} bind:tempIndex={tempIndex} bind:isAutoScrolling={isAutoScrolling} />
        <ScrollLink str={"Projects"} refStr={'projects'} bind:index={index} bind:tempIndex={tempIndex} bind:isAutoScrolling={isAutoScrolling} />
        <ScrollLink str={"Contact"} refStr={'contact'} bind:index={index} bind:tempIndex={tempIndex} bind:isAutoScrolling={isAutoScrolling} />
      </div>

    </div>
  </div>

  <!-- Placeholder for the fixed sidebar -->
  <div class="w-[260px] invisible"></div>
  {/if}


  <!-- Content -->
  <div class="flex-1 bg-blue-50">

    <!-- Mobile top bar -->
    {#if isMobile}
      <div bind:clientHeight={topbarHeight} class="fixed w-full z-[10]">
        <div class="bg-cyan-950 py-3 px-6 flex items-center gap-4">
          <div class="h-[46px] w-[46px] rounded-full">
            <!-- svelte-ignore a11y-img-redundant-alt -->
            <img class="rounded-full" src={profilePic} alt="Profile picture, Robin Salminen" >
          </div>

          <p class="text-white">Robin Salminen</p>
        </div>

        <div class="flex justify-around w-full bg-cyan-900 text-white pt-1">
          <ScrollLinkMobile str={"About me"} refStr={'about'} bind:index={index} bind:tempIndex={tempIndex} bind:isAutoScrolling={isAutoScrolling} />
          <ScrollLinkMobile str={"Projects"} refStr={'projects'} bind:index={index} bind:tempIndex={tempIndex} bind:isAutoScrolling={isAutoScrolling} />
          <ScrollLinkMobile str={"Contact"} refStr={'contact'} bind:index={index} bind:tempIndex={tempIndex} bind:isAutoScrolling={isAutoScrolling} />
        </div>
      </div>

      <!-- A dummy with the height of topbar -->
      <div style="height: {topbarHeight}px;"></div>
      
    {/if}

    <Scroller 
    {top}
    {threshold}
    {bottom}
    bind:index
    >


      <div slot="foreground">
        <section use:scrollRef={'about'} class="min-h-screen flex justify-center">
          <div class="w-[85%] md:w-[70%] flex flex-col gap-5 pt-6">

            <Header>About me</Header>

            <div class="flex flex-col gap-2">
              <Text>
                Welcome to my portfolio page! I'm Robin Salminen, a 26 year old Finnish engineer holding an
                MSc in Advanced Energy Conversions from Aalto University, completed with high honors. 
                My studies were heavily focused on energy conversion, fluid dynamics and programming. Additionally, I took part in other
                energy-related projects, which included designing a potential wind farm and investigating effects from the electrification road transport
                sector on the Finnish electricity grid.
                I currently work at ARKANCE as a software designer, and my tasks span from maintaining local IP software applications
                to developing new software applications in customer projects.
                The combination of my education and work experience has provided me a versatile set of skills applicable to various fields.
              </Text>

              <div>
                <Subheader>Technical skills</Subheader>

                <Text>
                  <span class="font-medium">General: </span>OpenFoam, Matlab, Simulink, Cantera, CI/CD
                </Text>
                <Text>
                  <span class="font-medium">Desktop Application Programming:</span> C, C++, C#, .NET, Avalonia UI, WPF, WinForms, Vulkan
                </Text>
                <Text>
                  <span class="font-medium">Web Application Programming, frontend:</span> JavaScript, TypeScript, ReactJS, Next.js, Svelte, Vue, Angular, Three.js
                </Text>
                <Text>
                  <span class="font-medium">Web Application Programming, backend:</span> .NET, Node.JS, SQL, NoSQL, Object Storage Service
                </Text>
              </div>

              <div>
                <Subheader>More</Subheader>
                <Text>
                  Feel free to check out the Projects -section, where I briefly present my master's thesis alongside some of my hobby projects. Links to the demo applications are provided.
                  You can also check out my <PopupLink href="https://github.com/RSalminen">GitHub</PopupLink>. 
                  While I keep most of my personal projects private, 
                  you can find the source code for this portfolio page there.
                  If you have any questions, my contact information can be found in the Contact -section.
                </Text>
              </div>
            </div>
          </div>
        </section>

        <section use:scrollRef={'projects'} class="w-full min-h-screen flex flex-col items-center pt-3">
          <div class="w-[85%] md:w-[70%] flex flex-col gap-5 pt-4">

            <Header>Projects</Header>
            <div>
              <Subheader classStr="mb-1">Master's thesis - A web-based application for visualizing CFD results</Subheader>
              
              <div class="py-1.5 md:px-5 flex justify-center lg:float-right">
                <img class="w-full sm:w-[300px] xl:w-[430px] rounded-md shadow-md shadow-gray-800" src={roomCW} alt="A CFD simulation displayed in the CFD Viewer Application">
              </div>
              
              <Text classStr="py-1.5">
                In my Master's thesis, made directly to Aalto University, I developed
                a web application for storing and displaying CFD results. The resulting application, named CFD Viewer,
                is used for educating computational fluid dynamics as it allows the student
                to easily view CFD simulation results posted by the teacher. The application
                also offers many customization options and a teaching notes system to help the teacher communicate
                information from the simulation results to the students.
              </Text>

              <Text classStr="py-1.5">
                The application consisted of a ReactJS frontend, a BackBlaze B2 object storage for storing the uploaded files,
                an SQL database for the user data and file identification and a Node.JS + ExpressJS API to handle communication between the frontend, database and the object storage.
                For reading the files and visualizing the data on the frontend, a WebGL -based data visualization library called vtk.js was used.
                The thesis contained detailed analysis on the ideal software architecture for data-heavy web applications,
                and presented ideas to further improve the performance and cost-efficiency of web applications that handle and visualize large amounts of data.
              </Text>

              <Text classStr="pt-1.5">
                CFD Viewer can be tried out at <PopupLink href="https://cfdwp.onrender.com/">https://cfdwp.onrender.com/</PopupLink>.
                Please keep in mind that this page is purely for demoing purposes. The application may be slow to load as it is deployed on free-of-charge infrastructure.
              </Text>
            </div>

            <div>
              <Subheader>Hobby projects</Subheader>
              
              <Text>
                In my spare time, I have done several small coding projects mainly for fun,
                but also to learn new technologies and to keep up with the rapidly developing space.
                Below are some examples which can easily be tested by opening the links.
              </Text>

              <ul class="list-disc py-2 px-6 text-[14px] md:text-[15px]">
                <!-- <li class="py-1">MarkkanenStats: a simple Next.js application that quickly shows statistics from Lauri Markkanen's most recent game. Uses Next.js API routes to connect to an external API for the data. Available at: <PopupLink href="https://markkanenstats.vercel.app/">https://markkanenstats.vercel.app</PopupLink></li>
                 -->
                <li class="py-1">Liikennehaukka: a ReactJS + ExpressJS fullstack application that finds the local traffic incidents, helping the user avoid traffic jams. Uses the traffic notice API by DigiTraffic. Available at: <PopupLink href="https://liikennehaukka.onrender.com/">https://liikennehaukka.onrender.com</PopupLink></li>
              </ul>
              
              
            </div>
          </div>
        </section>
        <section use:scrollRef={'contact'} class="w-full min-h-screen flex flex-col items-center pt-3">
          <div class="w-[85%] md:w-[70%] flex flex-col gap-5 pt-6">
            <Header>Contact</Header>

            <div class="flex mt-10 gap-3 h-7 items-center">
              <a class="p-3 bg-cyan-950 rounded-full hover:bg-cyan-900" href="mailto:robin.salminen@hotmail.com" target="_blank">
                <svg class="h-7 w-7 fill-white" stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 1024 1024" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M928 160H96c-17.7 0-32 14.3-32 32v640c0 17.7 14.3 32 32 32h832c17.7 0 32-14.3 32-32V192c0-17.7-14.3-32-32-32zm-40 110.8V792H136V270.8l-27.6-21.5 39.3-50.5 42.8 33.3h643.1l42.8-33.3 39.3 50.5-27.7 21.5zM833.6 232L512 482 190.4 232l-42.8-33.3-39.3 50.5 27.6 21.5 341.6 265.6a55.99 55.99 0 0 0 68.7 0L888 270.8l27.6-21.5-39.3-50.5-42.7 33.2z"></path></svg>
              </a>
              <a class="text-blue-700 hover:text-blue-900 hover:border-b-2 border-cyan-950  text-[15px] md:text-[17px]" href="mailto:robin.salminen@hotmail.com" target="_blank">robin.salminen@hotmail.com</a>
            </div>

            <div class="flex mt-8 gap-3 h-7 items-center">
              <a class="p-3 bg-cyan-950 rounded-full  hover:bg-cyan-900" href="https://github.com/RSalminen" target="_blank">
                <svg class="h-7 w-7 fill-white" stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 1024 1024" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M511.6 76.3C264.3 76.2 64 276.4 64 523.5 64 718.9 189.3 885 363.8 946c23.5 5.9 19.9-10.8 19.9-22.2v-77.5c-135.7 15.9-141.2-73.9-150.3-88.9C215 726 171.5 718 184.5 703c30.9-15.9 62.4 4 98.9 57.9 26.4 39.1 77.9 32.5 104 26 5.7-23.5 17.9-44.5 34.7-60.8-140.6-25.2-199.2-111-199.2-213 0-49.5 16.3-95 48.3-131.7-20.4-60.5 1.9-112.3 4.9-120 58.1-5.2 118.5 41.6 123.2 45.3 33-8.9 70.7-13.6 112.9-13.6 42.4 0 80.2 4.9 113.5 13.9 11.3-8.6 67.3-48.8 121.3-43.9 2.9 7.7 24.7 58.3 5.5 118 32.4 36.8 48.9 82.7 48.9 132.3 0 102.2-59 188.1-200 212.9a127.5 127.5 0 0 1 38.1 91v112.5c.8 9 0 17.9 15 17.9 177.1-59.7 304.6-227 304.6-424.1 0-247.2-200.4-447.3-447.5-447.3z"></path></svg>  
              </a>
              
              <a class="text-blue-700 hover:text-blue-900 hover:border-b-2 border-cyan-950  text-[15px] md:text-[17px]" href="https://github.com/RSalminen" target="_blank">github.com/RSalminen</a>
            </div>

            <div class="flex mt-8 gap-3 h-7 items-center">
              <a href="https://www.linkedin.com/in/robin-salminen-b01410173/" class="p-[14px] bg-cyan-950 hover:bg-cyan-900 rounded-full" target="_blank">
                <svg class="h-6 w-6 fill-white" stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 448 512" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M100.28 448H7.4V148.9h92.88zM53.79 108.1C24.09 108.1 0 83.5 0 53.8a53.79 53.79 0 0 1 107.58 0c0 29.7-24.1 54.3-53.79 54.3zM447.9 448h-92.68V302.4c0-34.7-.7-79.2-48.29-79.2-48.29 0-55.69 37.7-55.69 76.7V448h-92.78V148.9h89.08v40.8h1.3c12.4-23.5 42.69-48.3 87.88-48.3 94 0 111.28 61.9 111.28 142.3V448z"></path></svg>
              </a>
              
              <a class="text-blue-700 hover:text-blue-900 hover:border-b-2 border-cyan-950 text-[15px] md:text-[17px]" href="https://www.linkedin.com/in/robin-salminen-b01410173/" target="_blank">linkedin.com/in/robin-salminen-b01410173/</a>
            </div>
          </div>
        </section>
      </div>

    </Scroller>

  </div>
</main>

