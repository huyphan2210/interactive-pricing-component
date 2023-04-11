<script setup lang="ts">
import { ref } from 'vue';

const pageViews = ref(100);
const pricing = ref(16);
const yearPricing = ref(12)

const isYearBilling = ref(false);
const discountContent = ref(window.innerWidth / window.innerHeight > 1 ? '25% discount' : '-25%');
window.addEventListener('resize', handleResize);

function hanldeInput(e: Event) {
    const input = e.currentTarget as HTMLInputElement;
    pageViews.value = parseInt(input.value) * 2;
    pricing.value = 32 / 100 * parseInt(input.value);
    yearPricing.value = 24 / 100 * parseInt(input.value);
    input.setAttribute('style', `
        background: linear-gradient(to right, var(--soft-cyan) 0%, var(--soft-cyan) ${input.value}%, var(--light-grayish-blue-slider) ${input.value}%, var(--light-grayish-blue-slider) 100%);
        cursor: grabbing;`
    );
}

function handleToggle(e: Event) {
    const toggle = document.getElementsByClassName('toggle')[0];
    const circle = toggle.getElementsByTagName('div')[0]
    isYearBilling.value = !isYearBilling.value;
    if (circle.getAttribute('style')) {
        circle.style.left = '';
        toggle.setAttribute('style', '');
        
    } else {
        circle.style.left = 'calc(100% - 1.3rem)';
        toggle.setAttribute('style', 'background-color: var(--soft-cyan)');
    }
    
}

function handleResize() {
    discountContent.value = window.innerWidth / window.innerHeight > 1 ? '25% discount' : '-25%';
}

</script>

<template>
    <section>
        <div id="numbers">
            <h3>{{ pageViews }}K Pageviews</h3>
            <div id="pricing">
                <span>${{ isYearBilling ? yearPricing.toFixed(2) : pricing.toFixed(2) }}</span> / month
            </div>
        </div>
        <input type="range" title="Page views range" @input="hanldeInput">
        <div id="pricing-mobile">
                <span>${{ isYearBilling ? yearPricing.toFixed(2) : pricing.toFixed(2) }}</span> / month
            </div>
        <div id="billing">
            <p>Monthly Billing</p>
            <div class="toggle" @click="handleToggle">
                <div></div>
            </div>
            <p>Yearly Billing <span>{{ discountContent }}</span></p>
        </div>
    </section>
    <section>
        <div id="benefits">
            <div>
                <img src="../../assets/images/icon-check.svg" alt="Check">
                Unlimited websites
            </div>
            <div>
                <img src="../../assets/images/icon-check.svg" alt="Check">
                100% data ownership
            </div>
            <div>
                <img src="../../assets/images/icon-check.svg" alt="Check">
                Email reports
            </div>
        </div>
        <button type="button">Start my trial</button>
    </section>
</template>

<style scoped>
section {
    padding: 3rem;
}
    #numbers {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-block-end: 2rem;
    }
        #numbers h3 {
            text-transform: uppercase;
            letter-spacing: 0.1rem;
        }
        #pricing, #pricing-mobile {
            display: flex;
            align-items: center;
        }
        #pricing-mobile {
            display: none;
        }
        #pricing span, #pricing-mobile span {
            font-size: 3rem;
            font-weight: 800;
            margin-right: 0.5rem;
            color: var(--dark-desaturated-blue)
        }
        input {
            position: relative;
            z-index: 1;
            width: 100%;
            -webkit-appearance: none;
            appearance: none;
            background: linear-gradient(
                to right,
                var(--soft-cyan) 0%,
                var(--soft-cyan) 50%,
                var(--light-grayish-blue-slider) 50%,
                var(--light-grayish-blue-slider) 100%
            );
            cursor: pointer;
            height: 0.5rem;
            border-radius: 1rem;
        }

        input::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 2.5rem;
            aspect-ratio: 1;
            background-color: var(--strong-cyan);
            background-image: url(../../assets/images/icon-slider.svg);;
            background-repeat: no-repeat;
            border-radius: 50% 50%;
            background-position: 50%;
            box-shadow: 0 0 1rem var(--strong-cyan);
        }

            input::-webkit-slider-thumb:hover {
                filter: brightness(1.1);
            }

        #billing {
            position: relative;
            margin-block-start: 2rem;
            display: grid;
            grid-template-columns: 50% 50%;
            align-items: center;
            justify-content: center;
        }
            #billing p {
                margin-block: 0;
                text-align: end;
                margin-right: 2.5rem;
                font-size: 0.8rem;
            }

                #billing p:last-child {
                    white-space: nowrap;
                    text-align: start;
                    margin-left: 2.5rem;
                }

                #billing p:last-child span {
                    background-color: var(--light-grayish-red);
                    color: var(--light-red);
                    padding: 0.1rem 0.5rem;
                    border-radius: 1rem;
                }

            .toggle {
                position: absolute;
                width: 3rem;
                aspect-ratio: 2;
                background-color: var(--light-grayish-blue-bg);
                border-radius: 2rem;
                padding: 0.1rem;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
            }
                .toggle div {
                    position: absolute;
                    height: 1rem;
                    aspect-ratio: 1;
                    background-color: white;
                    left: 0.3rem;
                    top: 50%;
                    border-radius: 50%;
                    transform: translate(0, -50%);
                    transition: 0.5s;
                }
                .toggle:hover {
                    cursor: pointer;
                    background-color: var(--soft-cyan);
                }

    section:last-child {
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-block-start: solid 0.2rem var(--very-pale-blue);
    }
        button {
            padding: 1rem 2rem;
            border-radius: 2rem;
            border: none;
            background-color: var(--dark-desaturated-blue);
            color: var(--pale-blue);
        }

        button:hover {
            cursor: pointer;
            color: white;
        }

        #benefits div {
            margin-block-end: 1rem;
        }
            #benefits div:last-child {
                margin-block-end: 0;
            }

            #benefits div img {
                height: 100%;
                margin-right: 0.5rem;
            }

@media screen and (max-aspect-ratio: 1) {
    section {
        padding: 2rem;
    }

    section:last-child {
        flex-direction: column;
        text-align: center;
    }

    #numbers {
        justify-content: center;
    }

        #pricing {
            display: none;
        }

        #pricing-mobile {
            display: flex;
            align-items: center;
            justify-content: center;
        }

            #pricing-mobile span {
                font-size: 3rem;
            }
    input {
        margin-bottom: 2rem;
    }
    #benefits {
        margin-block-end: 2rem;
    }
    @media screen and (max-width: 280px) {
        #pricing-mobile span {
            font-size: 2rem;
        }

        #billing p:last-child {
            white-space: normal;
        }
    }
}
</style>
