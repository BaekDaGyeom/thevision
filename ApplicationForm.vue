<template>
    <div id="join_form">
        <!-- v-bind:style="{ 'background-image': url("/assets/images/background.png")}"  -->
        <h1>동아리 지원서</h1>
        <br>
        <form name="Application" method="post">
            <label for="name">이름 </label>
            <input type="text" id="name">
            <br><br>
            <label for="st_num">학번 </label>
            <input type="text" id="st_num">
            <br><br>
            <label for="ph_num">전화번호 </label>
            <input type="text" id="ph_num" placeholder=" - 없이 입력">
            <br><br>
            <label for="field">분야 </label>
            <input type="text" id="field">
            <br><br>
            <label for="dep">학과 </label>
            <input type="text" id="dep">
            <br><br>
            <label for="pass">비밀번호 </label>
            <input type="password" id="pass" placeholder="영문자+숫자+특수문자 조합">
            <br><br><br><br>
        </form>
        <div id="join_btn">
            <button type="button" id="submit" @click="joinform_check();">가입하기</button>
        </div>       
    </div>
    
</template>

<script setup>
    
    /* eslint-disable */
    
    import axios from 'axios'
    
    function joinform_check() {

        var Name = document.getElementById("name");
        var st_Num = document.getElementById("st_num");
        var ph_Num = document.getElementById("ph_num");
        var Field = document.getElementById("field");
        var Dep = document.getElementById("dep");
        var Pass = document.getElementById("pass");
        
        var kor_check = /[ㄱ-ㅎㅏ-ㅣ가-힣]/g; 
        var Tel_check = /^[0-9]{2,3}[0-9]{3,4}[0-9]{4}/;
        var Num_check = /^[0-9]+$/g;
        var Pass_check = /^(?=.*[a-zA-Z])(?=.*[!@#$%^*+=-])(?=.*[0-9]).{8,25}$/g;
        
        //이름 검사 (한글인지 판별)

        console.log(Name.value.match(kor_check));

        if(Name.value == ""){
            alert("이름을 입력하세요.");
            Name.focus();
            return false;
        };
        
        if(Name.value.match(kor_check) == null){
            alert("이름을 다시 입력하세요.");
            Name.focus();
            return false;
        }

        //학번 검사 (8자리 숫자인지 판별)

        console.log(st_Num.value.match(Num_check));

        if(st_Num.value == ""){
            alert("학번을 입력하세요.");
            st_Num.focus();
            return false;
        }

        if(st_Num.value.match(Num_check) == null || getDigit(st_Num.value) != 8){
            alert("학번을 다시 입력하세요.");
            st_Num.focus();
            return false;
        }

        //연락처 검사 (11자리 숫자인지 판별)

        console.log(ph_Num.value.match(Tel_check));

        if(ph_Num.value == ""){
            alert("전화번호를 입력하세요.");
            ph_Num.focus();
            return false;
        }

        if(ph_Num.value.match(Tel_check) == null || getDigit(ph_Num.value) != 11){
            alert("전화번호를 다시 입력하세요.");
            ph_Num.focus();
            return false;
        }

        //분야 검사

        if(Field.value == ""){
            alert("분야를 입력하세요.");
            Field.focus();
            return false;
        }

        //학과 검사

        if(Dep.value == ""){
            alert("학과를 입력하세요.");
            Dep.focus();
            return false;
        }

        //비밀번호 검사 (영어, 숫자, 특수문자 확인)

        console.log(Pass.value.match(Pass_check));

        if(Pass.value == ""){
            alert("비밀번호를 입력해주세요.");
            Pass.focus();
            return false;
        }
        
        if(Pass.value.match(Pass_check) == null){
            alert("비밀번호는 영문자+숫자+특수문자 조합으로 8~25자리 사용해야 합니다.");
            Pass.focus();
            return false;
        }



        // 숫자 자릿수 판별
        function getDigit(num) {
            num = num.toString();
            var i=0;
            while(num[i]) { i++; };
                return i;
        }  
        
        //document.Application.submit();

        axios.post('https://jsonplaceholder.typicode.com/users/', 
            {
                name: Name.value,
                st_num: st_Num.value,
                ph_num: ph_Num.value,
                field: Field.value,
                dep: Dep.value,
                pass: Pass.value
            }
            )
            .then(function (response) {
                console.log(response);
            })
            .catch(function (error) {
                console.log(error);
            });
        }


    

</script>

<style>
    
    @font-face {
        font-family: 'Tenada';
        src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2210-2@1.0/Tenada.woff2') format('woff2');
        font-weight: normal;
        font-style: normal;
    }

    @font-face {
        font-family: 'Humanbumsuk';
        src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2210-2@1.0/Humanbumsuk.woff2') format('woff2');
        font-weight: normal;
        font-style: normal;
    }

    body {
        background-image: url("C:\학교\동아리\thevision\src\assets\images\background.jpg");
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center;
    }

    h1 {
        font-size: 50px;
        font-family: 'Tenada';
        margin: 10px 0 30px 0;
        color: rgb(67, 88, 107);
    }

    #join_form {
        background-color: white;
        width: 900px;
        height: 500px;
        font-family: 'Humanbumsuk';
        font-size: 18px;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 70px;
        margin-top: 70px;
        text-align: center;
        padding: 50px 0px;
        color: rgb(16, 27, 48);
    }

    #submit {
        font-size: 20px;
        padding: 5px 10px;
        background-color: rgb(235, 246, 252);
        border-radius: 12px;
        border: 3px solid rgb(177, 217, 252);
        font-family: 'Tenada';
        margin: -20px 0 0 0;
        color: rgb(42, 54, 67);
    }

    #name, #st_num, #ph_num, #field, #dep, #pass {
        height: 20px;
        border-color: rgb(119, 190, 219);
        background-color: rgb(255, 255, 255);
        border-radius: 10px;
        font-family: 'Humanbumsuk';
        font-size: 17px;
        margin: 0 0 3px 15px;
    }
    
    #name {
        width: 100px;
    }
    #st_num {
        width: 120px;
    }
    #ph_num {
        width: 150px;
    }
    #field {
        width: 180px;
    }
    #dep {
        width: 150px;
    }
    #pass {
        width: 180px;
    }

</style>
