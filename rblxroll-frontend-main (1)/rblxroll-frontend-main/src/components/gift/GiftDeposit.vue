<template>
    <div class="gift-deposit">
        <div class="deposit-input">
            <input v-model="giftCode" type="text" placeholder="ENTER YOUR GIFTCARD CODE" />
            <button v-on:click="giftRedeemButton()">
                <div class="button-inner">REDEEM CARD</div>
            </button>
        </div>
        <div class="deposit-list">

            <GiftDepositElement v-bind:href="giftGetLink(3)" amount="3" />
            <GiftDepositElement v-bind:href="giftGetLink(5)" amount="5" />
            <GiftDepositElement v-bind:href="giftGetLink(10)" amount="10" />
            <GiftDepositElement v-bind:href="giftGetLink(25)" amount="25" />
            <GiftDepositElement v-bind:href="giftGetLink(50)" amount="50" />
            <GiftDepositElement v-bind:href="giftGetLink(100)" amount="100" />
            <GiftDepositElement v-bind:href="giftGetLink(250)" amount="250" />
            <GiftDepositElement v-bind:href="giftGetLink(500)" amount="500" />

        </div>
    </div>
</template>

<script>
    import { mapGetters, mapActions } from 'vuex';
    import GiftDepositElement from '@/components/gift/GiftDepositElement';

    export default {
        name: 'GiftDeposit',
        components: {
            GiftDepositElement
        },
        data() {
            return {
                giftCode: null
            }
        },
        methods: {
            ...mapActions([
                'notificationShow', 
                'modalsSetShow', 
                'modalsSetData'
            ]),
            giftGetLink(amount) {
                let link = null;

                if(this.modalsData.provider === 'kinguin') {
                    if(amount === 3) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; } 
                    else if(amount === 5) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 10) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 25) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 50) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 100) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 250) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 500) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                } else {
                    if(amount === 3) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; } 
                    else if(amount === 5) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 10) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 25) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 50) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 100) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 250) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                    else if(amount === 500) { link = 'https://www.paypal.com/ncp/payment/KVNKGAU8BHZGC'; }
                }

                return link;
            },
            giftRedeemButton() {
                if(this.giftCode === null || this.giftCode.trim() === '') {
                    this.notificationShow({ type: 'error', message: 'Your entered gift code is invalid.' });
                    return;
                }

                this.modalsSetShow(null);

                setTimeout(() => {
                    this.modalsSetData({ typeCaptcha: 'giftRedeem', data: { code: this.giftCode.replaceAll('-', '') } });
                    this.modalsSetShow('Captcha');
                }, 200);
            }
        },
        computed: {
            ...mapGetters([
                'modalsShow', 
                'modalsData'
            ])
        }
    }
</script>

<style scoped>
    .gift-deposit {
        width: 100%;
        margin-top: 35px;
    }

    .gift-deposit .deposit-input {
        width: 100%;
        height: 72px;
        position: relative;
        padding: 1px;
    }

    .gift-deposit .deposit-input::before {
        content: '';
        width: 100%;
        height: 72px;
        position: absolute;
        top: 0;
        left: 0;
        background: linear-gradient(180deg, #04131f 0%, #223a4e 100%);
        clip-path: polygon(14px 0, calc(100% - 14px) 0, 100% 25%, 100% 75%, calc(100% - 14px) 100%, 14px 100%, 0 75%, 0 25%);
    }

    .gift-deposit .deposit-input input {
        width: 100%;
        height: 70px;
        padding: 0 47px 0 15px;
        font-size: 16px;
        font-weight: 600;
        color: #ffffff;
        background-color: #072e3d;
        clip-path: polygon(14px 0, calc(100% - 14px) 0, 100% 25%, 100% 75%, calc(100% - 14px) 100%, 14px 100%, 0 75%, 0 25%);
    }

    .gift-deposit .deposit-input input::placeholder {
        color: #49687d;
    }

    .gift-deposit .deposit-input button {
        width: 147px;
        height: 47px;
        position: absolute;
        top: 50%;
        right: 12px;
        transform: translate(0, -50%);
    }

    .gift-deposit .deposit-input button .button-inner {
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 14px;
        font-weight: 800;
        color: #ffffff;
        background: linear-gradient(255deg, #00ffc2 0%, #00aa6d 100%);
        clip-path: polygon(8px 0, calc(100% - 8px) 0, 100% 25%, 100% 75%, calc(100% - 8px) 100%, 8px 100%, 0 75%, 0 25%);
    }

    .gift-deposit .deposit-list {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        margin-top: 10px;
    }

    @media only screen and (max-width: 500px) {

        .gift-deposit .deposit-input {
            height: auto;
        }

        .gift-deposit .deposit-input button {
            width: 100%;
            position: static;
            margin-top: 10px;
            transform: translate(0, 0);
        }

    }
</style>