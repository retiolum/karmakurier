<template>
    <div class="login-wrapper">
        <div class="form-wrapper">
            <div class="title">
                <span>Mega-schön</span> dich wiederzusehen!
            </div>
            <ValidationObserver v-slot="{ handleSubmit }">
                <div class="form">
                    <ValidationProvider
                        name="Telefon"
                        rules="required|min:5"
                        v-slot="{ errors, valid }"
                    >
                        <b-field
                            class="phone"
                            label="Telefon"
                            :type="{ 'is-danger': errors[0], 'is-success': valid }"
                            :message="errors"
                        >
                            <b-input v-model="loginData.phone"></b-input>
                        </b-field>
                    </ValidationProvider>

                    <ValidationProvider
                        name="Passwort"
                        rules="required|min:8"
                        v-slot="{ errors, valid }"
                    >
                        <b-field
                            class="password"
                            label="Passwort"
                            :type="{ 'is-danger': errors[0], 'is-success': valid }"
                            :message="errors"
                        >
                            <b-input type="password" v-model="loginData.password"></b-input>
                        </b-field>
                    </ValidationProvider>
                    <b-button class="btn" type="is-blue" @click="handleSubmit(login)">Jetzt anmelden</b-button>
                </div>
            </ValidationObserver>
        </div>
        <p>
            Du hast dein Passwort vergessen? Dann
            <router-link to="/passwort-vergessen">klick hier.</router-link>
        </p>
        <p>
            Du hast noch keinen Account? Dann
            <a href="/registrieren">registriere dich hier.</a>
        </p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            loginData: {
                phone: "",
                password: ""
            }
        };
    },
    methods: {
        login() {
            this.$store.commit("logIn", this.loginData);
            this.$router.go(-1); // go back
        }
    }
};
</script>

<style lang="scss" scoped>
@import "@/components/Branding.scss";

.login-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 40px 16px 64px 16px;
}

.form-wrapper {
    border-radius: 4px;
    overflow: hidden;
    // box-shadow: 0px 4px 8px rgba($primary, 0.24);
    width: 100%;
    max-width: 320px;
    @media only screen and (min-width: 560px) {
        width: 100%;
        max-width: 420px;
    }
    .title {
        // background-color: $primary;
        span {
            font-weight: 700;
            color: $blue;
        }
        padding: 16px;
    }
    .form {
        padding: 0 16px 16px 16px;
    }
}

p {
    width: 100%;
    max-width: 320px;
    margin-top: 12px;
    padding: 0px 16px;
    @media only screen and (min-width: 560px) {
        width: 100%;
        max-width: 420px;
    }
}
</style>
