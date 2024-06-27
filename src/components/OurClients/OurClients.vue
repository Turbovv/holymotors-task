<template>
    <div class="bg-black h-auto overflow-hidden py-8">
        <div class="text-center w-full h-auto place-items-center">
            <div class="h-full py-12">
                <h1 class="text-white text-3xl md:text-8xl font-black uppercase text-center mb-8">Clients</h1>

                <div class="wrapper mt-8">
                    <div class="scroll-container scroll-container-1">
                        <div v-for="(logos, index) in BrandLogos.slice(0, 6)" :key="'section1-' + index"
                            class="scroll-item">
                            <img class="w-12 md:w-16" :src="logos.image" :alt="logos.alt">
                        </div>
                        <div v-for="(logos, index) in BrandLogos.slice(0, 6)" :key="'section1-dup-' + index"
                            class="scroll-item">
                            <img class="w-12 md:w-16" :src="logos.image" :alt="logos.alt">
                        </div>
                    </div>
                </div>

                <div class="wrapper mt-8">
                    <div class="scroll-container scroll-container-2">
                        <div v-for="(logos, index) in BrandLogos.slice(6, 12)" :key="'section2-' + index"
                            class="scroll-item">
                            <img class="w-12 md:w-16" :src="logos.image" :alt="logos.alt">
                        </div>

                        <div v-for="(logos, index) in BrandLogos.slice(6, 12)" :key="'section2-dup-' + index"
                            class="scroll-item">
                            <img class="w-12 md:w-16" :src="logos.image" :alt="logos.alt">
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
import ClientsLogoImage1 from '../../assets/Clients_Logo_Images/client-logo-01.svg'
import ClientsLogoImage2 from '../../assets/Clients_Logo_Images/client-logo-02.svg'
import ClientsLogoImage3 from '../../assets/Clients_Logo_Images/client-logo-03.svg'
import ClientsLogoImage4 from '../../assets/Clients_Logo_Images/client-logo-04.svg'
import ClientsLogoImage5 from '../../assets/Clients_Logo_Images/client-logo-05.svg'
import ClientsLogoImage6 from '../../assets/Clients_Logo_Images/client-logo-06.svg'
import ClientsLogoImage7 from '../../assets/Clients_Logo_Images/client-logo-07.svg'
import ClientsLogoImage8 from '../../assets/Clients_Logo_Images/image-130.svg'
import ClientsLogoImage9 from '../../assets/Clients_Logo_Images/image-198.svg'
import ClientsLogoImage10 from '../../assets/Clients_Logo_Images/image-199.svg'
import ClientsLogoImage11 from '../../assets/Clients_Logo_Images/neon-logo 1.svg'
import ClientsLogoImage12 from '../../assets/Clients_Logo_Images/LOGO-1.svg'

export default {
    data() {
        return {
            BrandLogos: [
                {image: ClientsLogoImage1, alt: "Image 1"},
                {image: ClientsLogoImage2, alt: 'Image 2'},
                {image: ClientsLogoImage3, alt: 'Image 3'},
                {image: ClientsLogoImage11,alt:'Image 4'},
                {image: ClientsLogoImage8, alt: 'Image 5'},
                {image: ClientsLogoImage10, alt: 'Image 6'},
                {image: ClientsLogoImage7, alt: 'Image 7'},
                {image: ClientsLogoImage6, alt: 'Image 8'},
                {image: ClientsLogoImage4, alt: 'Image 9'},
                {image: ClientsLogoImage5, alt: 'Image 10'},
                {image: ClientsLogoImage9, alt: 'Image 11'},
                {image: ClientsLogoImage12, alt: 'Image 12'},
            ]
        };
    }
};
</script>

<style scoped>
@import '../../style.css';
*,
*::before,
*::after {
    box-sizing: border-box;
}
* {
    margin: 0;
}
.wrapper {
    width: 100%;
    margin-inline: auto;
    position: relative;
    height: var(--wrapper-height);
    overflow: hidden;
    mask-image: linear-gradient(to right,
            rgba(0, 0, 0, 0),
            rgba(0, 0, 0, 1) 20%,
            rgba(0, 0, 0, 1) 80%,
            rgba(0, 0, 0, 0));
}
.scroll-container {
    display: flex;
    align-items: center;
    width: calc(var(--item-width) * 12);
}
.scroll-item {
    width: var(--item-width);
    height: var(--item-height);
    display: flex;
    justify-content: center;
    align-items: center;
}
.scroll-container-1 {
    animation: scrollLeft var(--animation-duration-1) linear infinite;
}
.scroll-container-2 {
    animation: scrollRight var(--animation-duration-2) linear infinite;
}
@keyframes scrollLeft {
    0% {
        transform: translateX(0);
    }
    100% {
        transform: translateX(calc(var(--item-width) * -6));
    }
}
@keyframes scrollRight {
    0% {
        transform: translateX(calc(var(--item-width) * -6));
    }

    100% {
        transform: translateX(0);
    }
}
@media (min-width: 768px) {
    .wrapper {
        height: var(--md-wrapper-height);
    }
    .scroll-item {
        width: var(--md-item-width);
        height: var(--md-item-height);
    }
    .scroll-container {
        width: calc(var(--md-item-width) * 12);
    }
    @keyframes scrollLeft {
        0% {
            transform: translateX(0);
        }
        100% {
            transform: translateX(calc(var(--md-item-width) * -6));
        }
    }
    @keyframes scrollRight {
        0% {
            transform: translateX(calc(var(--md-item-width) * -6));
        }
        100% {
            transform: translateX(0);
        }
    }
}
</style>
