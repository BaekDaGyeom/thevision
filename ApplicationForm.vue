<template>

    <form name="Application" method="post">
        <label for="name">이름 </label>
        <input type="text" id="name">
        <br><br>
        <label for="st_num">학번 </label>
        <input type="text" id="st_num">
        <br><br>
        <label for="ph_num">전화번호 </label>
        <input type="text" id="ph_num">
        <br><br>
        <label for="field">분야 </label>
        <input type="text" id="field">
        <br><br>
        <label for="dep">학과 </label>
        <input type="text" id="dep">
        <br><br>
        <label for="pass">비밀번호 </label>
        <input type="password" id="pass" placeholder="영문자+숫자+특수문자 조합">
        <br><br>
    </form>
    <div class="join_btn">
        <button type="button" id="submit" @click="joinform_check();">가입하기</button>
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

</style>
