<template>

    <form name="Application" method="post">
        <label for="name">이름 </label>
        <input type="text" id="name">
        <br><br>
        <label for="st_num">학번 </label>
        <input type="text" id="st_num">
        <br><br>
        <label for="ph_num">전화번호 </label>
        <input type="tel" id="ph_num">
        <br><br>
        <label for="field">분야 </label>
        <input type="text" id="field">
        <br><br>
        <label for="dep">학과 </label>
        <input type="text" id="dep">
        <br><br>
        <label for="pass">비밀번호 </label>
        <input type="password" id="pass">
        <br><br>
    </form>
    <div class="join_btn">
        <button type="button" onclick="joinform_check();">가입하기</button>
    </div>

</template>

<script>
    /* eslint-disable */

    function joinform_check() {

        var Name = document.getElementById("name");
        var st_Num = document.getElementById("st_num");
        var ph_Num = document.getElementById("ph_num");
        var Field = document.getElementById("field");
        var Dep = document.getElementById("dep");
        var Pass = document.getElementById("pass");

        // var NameTrue = false;
        // var st_NumTrue = false;
        // var ph_NumTrue = false;
        // var FieldTrue = false;
        // var DepTrue = false;
        // var PassTrue = false;

        //이름 검사 (한글인지 판별)

        if(Name.value != ""){
            if(checkKor(Name) == true){
                if(checkSpace(Name) == false){
                    //NameTrue = true;                  
                }
            }
            else{
                alert("이름을 다시 입력해주세요.");
            }
        }
        else{
            alert("이름을 입력해주세요.");
        }
        //학번 검사 (8자리 숫자인지 판별)

        if(st_Num.value != ""){
            if(checkNum(st_Num) == true){
                if(checkSpace(st_Num) == false){
                    if(getDigit(st_Num) == 8){
                        //st_NumTrue = true;
                    }
                }      
            }
            else{
                alert("학번을 다시 입력해주세요.");
            }
        }
        else{
            alert("학번을 입력해주세요.");

        }

        //연락처 검사 (11자리 숫자인지 판별)

        var reg = /^[0-9]+/g;

        if(ph_Num.value != ""){
            if(getDigit(ph_Num) == 11){
                if(!reg.test(ph_Num) == true){
                    if(checkSpace(ph_Num) == false){
                        if(checkSpecial(ph_Num) == false){
                            //ph_NumTrue = true;
                        }
                    }
                }
            }
            else{
                alert("연락처를 다시 입력해주세요.");
            }
        }
        else{
            alert("연락처를 입력해주세요.");

        }

        //분야 검사 (한글, 영문 판별)

        if(Field.value != ""){
            if(checkKor(Field) == true || checkEng(Field) == true){
                //FieldTrue = true;
            }
            else{
                alert("분야를 다시 입력해주세요.")
            }
        }
        else{
            alert("분야를 입력해주세요.")

        }

        //학과 검사 (한글, 영문 판별)

        if(Dep.value != ""){
            if(checkKor(Dep) == true || checkEng(Dep) == true){
                //DepTrue = true;
            }
            else{
                alert("학과를 다시 입력해주세요.")
            }
            }
        else{
            alert("학과를 입력해주세요.")

        }

        //비밀번호 검사 (영어, 숫자, 특수문자 확인)

        if(Pass.value != ""){
            if(checkEng(Pass) == true){
                if(checkNum(Pass) == true){
                    if(checkSpecial(Pass) == true){
                        //PassTrue = true;
                    }
                }
            }
            else{
                alert("비밀번호를 다시 입력해주세요.")
            }
        }
        else{
            alert("비밀번호를 입력해주세요.")

        }

        document.join_form.sublit();
   
     }





// 숫자 자릿수 판별
function getDigit(num) {
  num = num.toString();
  var i=0;
  while(num[i]) { i++; };
  return i;
}   

// 특수 문자 체크 
     function checkSpecial(str) { 
     const regExp = /[!?@#$%^&*():;+-=~{}<>\_\[\]\|\\\"\'\,\.\/\`\₩]/g;
    if(regExp.test(str)) {
        return true;
    }else{
    } 
} 

// 한글 체크
function checkKor(str) {
    const regExp = /[ㄱ-ㅎㅏ-ㅣ가-힣]/g; 
    if(regExp.test(str)){
        return true;
    }else{
    }
}

// 숫자 체크
function checkNum(str){
    const regExp = /[0-9]/g;
    if(regExp.test(str)){
        return true;
    }else{
    }
}

// 영문(영어) 체크
function checkEng(str){
    const regExp = /[a-zA-Z]/g; // 영어
    if(regExp.test(str)){
        return true;
    }else{
    }
}

// // 영문+숫자만 입력 체크
// function checkEngNum(str) {
//     const regExp = /[a-zA-Z0-9]/g;
//     if(regExp.test(str)){
//         return true;
//     }else{
//      
//     }
// }


// 공백(스페이스 바) 체크
function checkSpace(str) { 
    if(str.search(/\s/) !== -1) {
        return true; // 스페이스가 있는 경우
    }else{ // 스페이스 없는 경우
    } 
}



</script>

<style>

</style>

