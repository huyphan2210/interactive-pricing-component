<script setup lang="ts">
import { ref } from 'vue';

const pageViews = ref(100);
const pricing = ref(16);
const yearPricing = ref(12)

const isYearBilling = ref(false);
const discountContent = ref(window.innerWidth / window.innerHeight > 1 ? '25% discount' : '-25%');
window.addEventListener('resize', handleResize);

function hanldeInput(e: Event) {
    pageViews.value = parseInt((e.currentTarget as any).value) * 2;
    pricing.value = 32 / 100 * parseInt((e.currentTarget as any).value);
    yearPricing.value = 24 / 100 * parseInt((e.currentTarget as any).value);
    document.getElementsByTagName('input')[0].setAttribute('style', `background: linear-gradient(to right, var(--soft-cyan) 0%, var(--soft-cyan) ${(e.currentTarget as any).value}%, var(--light-grayish-blue-slider) ${(e.currentTarget as any).value}%, var(--light-grayish-blue-slider) 100%);`);
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
        #pricing {
            display: flex;
            align-items: center;
        }
        #pricing span {
            font-size: 3rem;
            font-weight: 800;
            margin-right: 0.5rem;
            color: var(--dark-desaturated-blue)
        }
        input {
            position: relative;
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
            background-repeat: no-repeat;
            border-radius: 50%;
        }

        input::before {
            position: absolute;
            content: '';
            background-image: url(../../assets/images/icon-slider.svg);
            width: 2rem;
            aspect-ratio: 1;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-repeat: no-repeat;
            background-position: 50%;
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
        padding: 1rem;
    }

    section:last-child {
        flex-direction: column;
        text-align: center;
    }

    #benefits {
        margin-block-end: 2rem;
    }
}
</style>
