# Firebase 회원가입 에러



firebase를 이용해 회원가입을 하던 도중 오류가 났다.

```kotlin
fun doSignUpEmail() {
        firebaseAuth.createUserWithEmailAndPassword(signupId.toString(),signupPw.toString())
            .addOnCompleteListener(signUpEmailActivity) {
                if (it.isSuccessful) {
                    signUpEmailSuccessLiveEvent.call()
                } else {
                    signupEmailFailedLiveEvent.call()
                }
            }
            .addOnFailureListener {
                Log.d("DEBUGLOG", it.toString())
            }
    }
```

이 코드는 회원가입을 하는 코드인데, 400 코드의 오류가 났다.

찾아보니 400은 JSON을 이용한 통신에 오류가 있을 때 나오는 코드인데 오류를 찾아도 생각이 나지 않았다.

그래서 .addOnFailureListener를 달아서 오류명을 확인해보니

D/DEBUGLOG: com.google.firebase.auth.FirebaseAuthInvalidCredentialsException: The email address is badly formatted.

이메일 형식이 잘못되었다는 것이였다.

그래서 이메일을 보니 나는 signupId의 value 값을 받아와야했는데 signupId만을 받아오고 있어서 형식에 오류가 있었던 것이였다.

그래서 이렇게 수정했다.

```kotlin
fun doSignUpEmail() {
   firebaseAuth.createUserWithEmailAndPassword(signupId.value.toString(),signupPw.value.toString())
            .addOnCompleteListener(signUpEmailActivity) {
                if (it.isSuccessful) {
                    signUpEmailSuccessLiveEvent.call()
                } else {
                    signupEmailFailedLiveEvent.call()
                }
            }
            .addOnFailureListener {
                Log.d("DEBUGLOG", it.toString())
            }
    }
```

이랬더니 값이 잘 들어오는 모습을 볼 수 있었다.

![1593999164665](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1593999164665.png)