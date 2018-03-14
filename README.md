# help-me-fix-my-project
"auth/argument-error" message : "signInWithEmailAndPassword failed: Second argument "password" must be a valid string." __proto__ : Error


<---here are my codes(HTML)--->
 <dialog class="mdl-dialog">
    <h4 class="mdl-dialog__title">Sign In</h4>
    <div class="mdl-dialog__content">
      <p id="loginerror"></p>
      <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
        <input class="mdl-textfield__input" type="text" id="loginemail">
        <label class="mdl-textfield__label" for="sample3">Email...</label>
      </div>
      <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
        <input class="mdl-textfield__input" type="Password" id="loginpassword">
        <label class="mdl-textfield__label" for="sample3">Password...</label>
      </div>
    </div>
    <div class="mdl-dialog__actions">
      <button id="loginbtn" class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored mdl-js-ripple-effect">
  Sign In
</button>
<div id="loginprogress" class="mdl-spinner mdl-js-spinner is-active"></div>
    </div>
  </dialog>
  <div class="login-cover">
            <div class="mdl-spinner mdl-spinner--single-color mdl-js-spinner is-active"></div>
        </div>
<---Javascript--->
firebase.auth().onAuthStateChanged(function(user) {
  if (user) {
    // User is signed in.
    $(".login-cover").hide();
    if (! dialog.showModal) {
      dialogPolyfill.registerDialog(dialog);
    }
    
    dialog.close();
  } else {
    // No user is signed in.
    var dialog = document.querySelector('dialog');
    
   if (! dialog.showModal) {
      dialogPolyfill.registerDialog(dialog);
    }
    
    dialog.showModal();
   
  }
});

$("#loginbtn").click(
  function(){
    
    var email = $("#loginemail").val();
    var password = $("loginpassword").val();

    if (email !="" && password !="") {
      $("#loginprogress").show();
      $("#loginbtn").hide();

      firebase.auth().signInWithEmailAndPassword(email, password).catch(function(error){
        // Handle Errors here.

        $("#loginerror").show().text(error.message);

        $("#loginprogress").hide();
        $("#loginbtn").show();
        // ...
      });
    }
  }
);
