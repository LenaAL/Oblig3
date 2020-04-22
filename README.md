# Oblig3
local storage/ validate form
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profile</title>
</head>

<body onload="displayProfile()">


    <h1>Profile</h1>

    Your Name
    <form name="Login" method="post" action="#" onsubmit="return validateForm()">

        <input type="text" name="fName" id="FN"> <br>

        Age <br>
        <input type="text" name="ageField" id="age"> <br>

        Email <br>
        <input type="text" name="email" id="e"><br>

        Number <br>
        <input type="text" name="number" id="num">


        <input onclick="UpdateProfile();" type="submit" name="sub" value="Update">

    </form>


    <script type="text/javascript">

        class Profile {

            setProfile(n, a, e, t) {
                this.name = n;
                this.age = a;
                this.email = e;
                this.telephoneNumber = t;

                this.saveProfile();
            }

            getProfile() {
                document.getElementById("FN").value = localStorage.getItem('name');
                document.getElementById("age").value = localStorage.getItem('age');
                document.getElementById("e").value = localStorage.getItem('email');
                document.getElementById("num").value = localStorage.getItem('number');
            }

            saveProfile() {
                let storeName = document.getElementById('FN').value;
                localStorage.setItem('name', storeName);
                let storeAge = document.getElementById('age').value;
                localStorage.setItem('age', storeAge);
                let storeEmail = document.getElementById('e').value;
                localStorage.setItem('email', storeEmail);
                let storeNum = document.getElementById('num').value;
                localStorage.setItem('number', storeNum);
                alert('Data succesfully saved in localStorage');
            }

        }
        //Validate forms
        function validateForm() {

            var x = document.forms['Login']['fName'].value;
            if (x == null || x == "") {
                alert("Please enter your name");
                document.getElementById('FN').focus();
                //return false;
            } else if (x.length < 3) {
                alert("Your name must be 3 or more characters");
                document.getElementById("FN").focus();
                //return false
            }

            a = document.forms['Login']['ageField'].value;
            if (a == null || a == "") {
                alert("Age can not be empty");
                document.getElementById('age').focus();
                //return false;
            }
            else if (parseInt(a) < 12 || parseInt(a) > 95) {
                alert("Your age should be between 12 and 95");
                document.getElementById('age').focus();
                //return false;
            }

            var em = document.forms['Login']['email'].value;
            var atpos = em.indexOf("@");

            var dotpos = em.lastIndexOf(".");
            // Compare the numerical values
            if (atpos < 1 || dotpos < atpos + 4 || dotpos + 2 >= em.length) //spør om det er riktig med + 4 for fire tall ntny
            {
                alert("Not a valid e-mail address");
                //return false;
            } else if (em == null || em == "") {
                alert("Please enter your email adress");
                document.getElementById('e').focus();
                //return false;
            }

            var numb = document.forms['Login']['number'].value;
            if (numb == null || numb == "") {
                alert("Please enter your phone number");
                document.getElementById('num').focus();
                //return false;
            } else if (numb.length > 7) {
                alert("Phone number cannot be more than 7 digits");
                document.getElementById('num').focus();
                //return false;
            }
            return true; //usikker om den ska vær m
        }

        function UpdateProfile() {
            myProfile = new Profile;
            if (validateForm()) {
                myProfile.setProfile();
            }
        }

        function displayProfile() {
            dp = new Profile()
            dp.getProfile();
        }

    </script>
</body>

</html>
