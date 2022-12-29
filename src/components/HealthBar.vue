<template>
    <div class="health-container">
        <div class="text-container">
            <p class="characteristic">
                <span class="icon icon-health"></span>
                Health count: {{ healthCount }}
            </p>
            <p class="characteristic">
                <span class="icon icon-attack"></span>
                Hit power: {{ hitPower }}
            </p>
            <p class="characteristic">
                <span class="icon icon-regen"></span>
                HP Regen: {{ hpRegen }}
            </p>
        </div>

        <div class="bar">
            <div class="health__white" :style="'right:' + damageWhite + '%'"></div>
            <div class="health" :style="'right:' + damagePercent + '%'"></div>
            <p class="health__count dota-text">
                {{ Math.ceil(health) }}
                <span v-if="!health">You died</span>
            </p>
        </div>
        <div class="button-container">
            <HitButtons :button-text="'Hit'" :callback="hit" />
            <HitButtons :button-text="'Heal'" :callback="heal" />
        </div>
        <form action="javascript:void(0);" class="input-container">
            <TextInput :placeholder-text="'HP Count'" @postingValue="healthGet" />
            <TextInput :placeholder-text="'Hit Power'" @postingValue="attackGet" />
            <TextInput :placeholder-text="'HP Regen'" @postingValue="hpRegenGet" />
        </form>
    </div>
</template>
  
<script>
import HitButtons from './HitButtons.vue';
import TextInput from './TextInput.vue';

export default {
    name: 'HealthBar',

    props: {
    },

    components: {
        HitButtons,
        TextInput
    },

    data() {
        return {
            health: 0,
            hpRegen: 0,
            damagePercent: 100,
            damageWhite: 100,
            hitPower: 0,
            timersArr: [],
            healthCount: 0,
        }
    },

    methods: {
        hit() {
            if (this.damagePercent <= 100) {
                this.damagePercent += (Math.ceil(this.hitPower / this.healthCount * 100 * 100) / 100);
                // this.damagePercent += this.hitPower / this.healthCount * 100;
                this.health <= this.hitPower ? this.health = 0 : this.health -= this.hitPower;

                const timerID = setTimeout(this.whiteHit, 150);
                this.timersArr.push(timerID);
                this.clearTimers();
                console.log(this.healthCount, this.health, this.hitPower);
                if (this.healthCount - this.health == this.hitPower) {
                    this.regen();

                }
            } else return;
        },

        heal() {
            this.damagePercent = 0;
            this.damageWhite = 0;
            this.health = this.healthCount;
        },

        whiteHit() {
            this.damageWhite = this.damagePercent;
        },

        clearTimers() {
            if (this.timersArr.length > 1) {
                for (let i = 0; i < this.timersArr.length - 1; i++) {
                    clearTimeout(this.timersArr[i]);
                }
            }
        },

        regen() {
            let timerArr = 0;
            if (Math.ceil(this.health) >= this.healthCount) {
                clearTimeout(timerArr);
                this.damagePercent = 0;
                this.damageWhite = 0;
                this.health = this.healthCount;
            } else if (Math.floor(this.health) == 0) {
                clearTimeout(timerArr);
                this.damagePercent = 100;
                this.damageWhite = 100;
            } else {
                this.health += Math.ceil(this.hpRegen / 10 * 100) / 100;
                this.damagePercent -= Math.ceil(this.hpRegen / this.healthCount * 100 * 100) / 1000;
                this.damageWhite -= Math.ceil(this.hpRegen / this.healthCount * 100 * 100) / 1000;
                const timerID = setTimeout(this.regen, 100);
                timerArr = parseInt(timerID);
            }
        },

        healthGet(data) {
            this.health = parseInt(data);
            this.healthCount = parseInt(data);
            this.damagePercent = 0;
            this.damageWhite = 0;
        },

        attackGet(data) {
            this.hitPower = parseInt(data);
        },

        hpRegenGet(data) {
            this.hpRegen = parseInt(data);
        }
    }
}
</script>
  
 
<style lang="scss" scoped>
p {
    margin: 0;
    @include fontNunito(1.2rem);
    color: $color-text-color;
    text-shadow: 1px 1px 10px $color-interface;
}

.dota-text {
    @include fontTrajan(2rem);
}

.text-container {
    display: flex;
    justify-content: flex-start;
    gap: 15px;
    align-self: flex-start;
    margin-bottom: -15px;
}

.health-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 30px;
    box-sizing: border-box;
    width: 100%;
}

.bar {
    width: 100%;
    height: 60px;
    border: 2px solid $color-interface;
    overflow: hidden;
    background-color: $color-interface;
    position: relative;
}

.health__white,
.health {
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0%;
    right: 0%;
    transition: right 0.1s;
}

.health__white {
    background-color: $color-hit;
    z-index: 1;
}

.health {
    background-color: $color-health;
    z-index: 2;
    transition: right 0.05s;
}

.health__count {
    font-size: 2.0rem;
    text-shadow: 1px 1px 10px $color-interface;
    color: $color-text-color;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 3;
}

.button-container {
    display: flex;
    gap: 30px;
}

.input-container {
    min-width: 200px;
    display: flex;
    flex-direction: column;
    gap: 15px;
    background-color: $color-bg-300;
}

.characteristic {
    display: flex;
    align-items: center;
    gap: 8px;
}

.icon {
    display: block;
    width: 40px;
    height: 30px;

    &-health {
        background: url(../assets/icon/health.png) center center no-repeat;
        background-size: cover;
    }

    &-attack {
        background: url(../assets/icon/attack.png) center center no-repeat;
        background-size: cover;
    }

    &-regen {
        background: url(../assets/icon/regen.png) center center no-repeat;
        background-size: cover;
    }
}
</style>
  