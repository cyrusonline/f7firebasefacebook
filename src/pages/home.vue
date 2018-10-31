<template>
<f7-page>
    <f7-navbar sliding title="Home"></f7-navbar>
    <f7-block-title>{{ title }}</f7-block-title>
    <f7-block inner>
        <f7-button @click="login">login</f7-button>
        <f7-button @click="logout">logout</f7-button>
    </f7-block>
</f7-page>
</template>

<script>
import firebase from 'firebase';
var config = {
    apiKey: "AIzaSyBFmys2X9eU-VUzJ75B2VpIW41YJaEkmmI",
    authDomain: "yrmentor2018.firebaseapp.com",
    databaseURL: "https://yrmentor2018.firebaseio.com",
    projectId: "yrmentor2018",
    storageBucket: "yrmentor2018.appspot.com",
    messagingSenderId: "176560638600"
};
firebase.initializeApp(config);
firebase.firestore().settings({
    timestampsInSnapshots: true
})
export default {
    name: 'Home',
    data() {
        return {
            title: 'Hello World'
        };
    },
    methods: {
        login() {
            let provider = new firebase.auth.FacebookAuthProvider();
            firebase.auth().signInWithRedirect(provider).then(function () {
                return firebase.auth().getRedirectResult();
            }).then(function (result) {
                // This gives you a Google Access Token.
                // You can use it to access the Google API.
                var token = result.credential.accessToken;
                // The signed-in user info.
                var user = result.user;
                alert(JSON.stringify(result))
                console.log(result)
                // ...
            }).catch(function (error) {
                // Handle Errors here.
                var errorCode = error.code;
                var errorMessage = error.message;
            });
        },
        logout() {
            firebase.auth().signOut().then(function () {
                alert('signouted')
            }).catch(function (error) {
                // An error happened.
            });
        }
    }
};
</script>
