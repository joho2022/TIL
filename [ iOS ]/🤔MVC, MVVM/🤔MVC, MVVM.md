# ๐ค MVC, MVVM

<img width="675" alt="แแณแแณแแตแซแแฃแบ 2023-02-07 แแฉแแฅแซ 12 52 09" src="https://user-images.githubusercontent.com/104732020/220582681-9ec32827-9356-4912-9e13-1c5e4396981f.png">

์์ ๊ทธ๋ฆผ์ ์ ํ ๋ฌธ์์์ ๊ฐ์ด๋ํ๋ MVC๊ตฌ์กฐ์ด๋ค. 

MVC๋ ๊ทธ๋ฆผ์ฒ๋ผ Model View Controller์ ์ฝ์์ด๋ค.  

Model์ ์ด๋ค ๋ฐ์ดํฐ๋ค

View๋ ์ค์  ์ฌ์ฉ์์๊ฒ ๋ณด์ฌ์ง๋ ๋ทฐ๋ค

๊ทธ ์ฌ์ด์ View Controller๊ฐ ์ปจํธ๋กค ์ญํ ์ ํ๋ฉด์ ๋ชจ๋ธ๊ณผ ๋ทฐ์ฌ์ด์ ์ํธ์์ฉ์ ํ๋ค.

์ ํ์ด ๊ฐ์ด๋ํด์ค๋๋ก MVCํจํด์ ์ ์ฐ๋ฉด์ ์๊ด์ด ์์ง๋ง ์ค์ ๋ก UIkit์์ View๋ ViewController๋ฅผ ์ฌ์ฉํด๋ณด๋ฉด View๋  ViewController๊ฐ ์๋นํ ์์ฒญ ๊ฐ๊น๋ค. 

์ธ๊ฐ์ง ๋ฉ์ด๋ฆฌ๊ฐ ๊ฐ๊ฐ ์๋ ๊ฒ์ฒ๋ผ ๋ณด์ฌ์ง์ง๋ง ๋ทฐ์ ๋ทฐ์ปจํธ๋กค๋ฌ๊ฐ ์์ฒญ ๋ถ์ด์๋ค.

![Untitled](https://user-images.githubusercontent.com/104732020/220595811-4d988c88-f469-41f3-84e1-839cb608bde2.png)


๊ทธ๋ฌ๋ค๋ณด๋ ์ ๊ทธ๋ฆผ๊ณผ ๊ฐ์ด ํํ๋๋๊ฒ ์ข ๋ ํ์ค๋ชจ์ต์ ๋ด๊ณ  ์๋ค.

์ด๋ฌ๋ค๋ณด๋ View Controller์ ๋ง์ ๋ก์ง์ด ์กด์ฌํ๊ฒ ๋๋ ๊ฒฝ์ฐ๊ฐ ์๋ค.

์๋ฅผ ๋ค์ด

- ํ๋ ์  ํ์ด์ ๋ก์ง
- ๋น์ฆ๋์ค ๋ก์ง
- ๋ฐ์ดํฐ ์ ๊ทผ ๋ก์ง
- ๋ฑ๋ฑ

์ด๋ฌํ ๋ทฐ์ปจํธ๋กค๋ฌ๊ฐ ์ ์  ๋น๋ํด์ง๋๋ฐ .. ์ ํ์ด ์ํค๋๋๋ก ํ์ง๋ง ๊ตฌ์กฐ์ ์ผ๋ก ๋ทฐ์ปจํธ๋กค๋ฌ๊ฐ ์ปค์ง๋ ๊ตฌ์กฐ๋ฅผ 

๊ฐ์ก์ผ๋๊น ์ฌ๋๋ค์ด ๋๋ฆฌ๋ ์ฉ์ด๋ก **M**assive **V**iew**C**ontroller ์๊น

## ์์ ๊ฐ์ ์ด์ ๋ก ๋ฐ์ํ๋ ๋ฌธ์ 

- view Controller๊ฐ ๋๋ฌด ๋ง์ ์ฑ์์ ์ง๊ณ  ์๋ค.

์๋ฅผ ๋ค๋ฉด ํ๊ธ์ ์๋ ๋ฐ์ฅ์ด ์ฌ๋ฌ๊ฐ์ง ์ญํ ์ ํ๊ฒ ๋๋ฉด ํ๋ค์ด์ง๋ ๊ฒ์ฒ๋ผ  

๋ทฐ์ปจํธ๋กค๋ฌ๊ฐ ๋๋ฌด ๋ง์ ์ญํ ์ ํ๊ฒ ๋๋ฉด ํ๋ค์ด์ง๋ค. ( ๋์ค์๋ ๊ฐ๋นํ  ์ ์์ด์ง.. ๊ฐ๋ฐ์๋ค๋ ) ๊ทธ๋ฌ๋ค๋ณด๋

์ ์ง๋ณด์๊ฐ ์ด๋ ค์ด ๊ฒฝ์ฐ๊ฐ ์๊ธด๋ค.

- ๋ชจ๋ธ(๋ฐ์ดํฐ)๋ฅผ ์ง์  ์ ๊ทผํ๋ฉด์ ์์ ํ๋ค๋ณด๋, ๋ฒ๊ทธ์ ์ทจ์ฝํ๊ฒ ๋จ.

๊ฒฐ๊ตญ ๋น๋ํด์ง ๋ทฐ์ปจํธ๋กค๋ฌ๋ ๋ง์น ์ฌ๋ฌ๊ฐ์ง ๋ฌธ์ ๋ฅผ ๋ด๊ณ ์๋ **ํญํ**๊ณผ ๊ฐ๋ค.

## ๐ค๊ทธ๋์ ๋ฌธ์ ๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด์

ViewController๋ฅผ View๋ ์ด์ด๋ก ์ดํดํ์ ๊ทธ๋ฌ๋ฉด View๋ ์ด์ด์์๋ ์ด๋ค ์ผ์ ํด์ผํ๋๋ฉด

- ๋ฐ์ดํฐ๋ฅผ ๋ทฐ์ ํ์ํ๋ค
- ์ฌ์ฉ์ ์ธํฐ๋ ์์ ๋ฐ์์ ์ฒ๋ฆฌํด์ฃผ๋ ๋์์๊ฒ ๋์ ธ์ค๋ค.

(๊ทธ๋์ ๋ทฐ์ปจํธ๋กค๋ฌ๊ฐ ๋ง์ ์ผ์ ํ๋คโฆ)

View ๋ ์ด์ด์ ์๋ง์ ํํ๋ก Model์ ๊ฐ๊ณตํด์ ์ ๋ฌํ์.

- ์ฆ, ViewModel๋ก ์ ๊ณตํ์

์๋ฅผ ๋ค์ด Model์ Data ํ์์ด ์๋ค๋ฉด ํ๋ฉด์ ๋ณด์ฌ์ค๋๋ Stringํ์์ผ๋ก ๋ณด์ฌ์ค์ผ ํ๋ ๊ทธ๋ฐ๊ฑธ๋ก ๋ณํ๋์ด  

์๋ ํํ์ฒ๋ผ ์ด๋ฌํ ๊ฒ์ ViewModel์ ํ์์ ํตํด์ ๋ณํ์์ผ์ฃผ๋ฉด ๋๋ค. 

๊ทธ๋ฆฌ๊ณ  ViewModel์๋ ์ ๋ง View์ ํ์ํ ViewModel๋ค์ ๋ง๋ค์ด์ฃผ๊ธฐ๋ ํ๊ณ  ๊ฐ์ข ๋ชจ๋ธ๋ค์ ๋ทฐ๋ชจ๋ธ์ ํตํด์  ๋ทฐ์ ๊ฝ์์ฃผ๋ ํํ๋ก ๋ง๋ค์ด์ฃผ๋ ์ฌ์ด์ ํ์ํ ๊ฐ์ข Controller ๋ฐ Manager๊ฐ ์์ ์ ์๋ค.

์ด๋ฌํ ๊ฒ๋ค์ View ๋ ์ด์ด๊ฐ ๋ชจ๋ฅด๊ฒ ํด์ผํ๋ค. ๊ทธ๋์ View๋ ViewModel์ด ๋ ๋จน์ฌ์ฃผ๋ ๊ฒ๋ง ๋จน๋ ๊ฒ์ฒ๋ผ..

View๊ฐ โ๋คํธ์ํฌ ์ด๋ ๊ฒ ํด์ผํ๋๊ฑฐ ์๋์ผ?โ, โDB์ ๊ทผํด์ ํด์ผ๋๋๊ฑฐ ์๋์ผ?โ๋ผ๋ ๋ฅ๋์ ์ธ ํ๋์ ์ต๋ํ

์์ ํ๊ฒ ํ๋ค. ์๋ํ๋ฉด ๋ค๋ฅธ ๊ฐ์ฒด๋ค์ ๋ง๋ค์ด์ ๊ฑ๋ค์๊ฒ ์ฑ์์ ์ค๊ฑฐ์ด๊ธฐ ๋๋ฌธ์ ์ ๋ง View๋ ๋ฐ๋ณด๋ก ๋ง๋ค์ด์ผ ํ๋ค.

### ๊ฒฐ๋ก ์ ์ผ๋ก ViewModel์ ๋ง๋ค์ โ ๊ธฐ์กด์ ๋ฌธ์ ํด๊ฒฐ

MVVM์ ์ฝ์๋

Model - View - ViewModel 

![Untitled (1)](https://user-images.githubusercontent.com/104732020/220595975-fb0a8f35-99c4-4c1b-bd61-6a0ed613b0f7.png)


View๋ ์ด์ด๋ Model๊ณผ ์ง์  ํต์ ํ์ง ์๋๋ค.

View Controller๋ ViewModel์ ๋ค๊ณ  ์๊ณ 

View Model์ Model์ ๋ค๊ณ  ์๋ค.

## View Model์ ์ด๋ค ์ญํ ์ ํ๋?

### 1. Data โ Output

- Model(Data) ๋ฅผ ๊ฐ์ง๊ณ  ์๊ณ ,
    - View ์ ์ ์ฉํ ์ ์๋๋ก ๊ฐ๊ณต๋์ด ์์
    - ๋ฐ์ดํฐ๋ฅผ ๊ฝ์์ฃผ๋ ์ญํ ์ ํ๊ณ  ์๋ค

### 2. User Action โ Input

- User Action ์ ๋ํ ์ฒ๋ฆฌ๋ฅผ ๋ด๋นํจ
    - ์ค์  ์ก์์ ๋ํด์๋ View ๊ฐ ์๋ ค์ค
    
    - ๋ค๋ง ์ก์์ผ๋ก ์ํ๋์ด์ผ ํ๋ ๋น์ฆ๋์ค ๋ก์ง์ ์ฒ๋ฆฌํจ

View์๋ค๊ฐ ๋ ๋จน์ฌ์ค์ผ ํ๋๊น View์ ์ด๋ค ๋ชจ๋ธ๋ค์ ๋ฐ๋ก ๊ฝ์ ์ ์๋๋ก ๊ฐ๊ณตํ๋ ์์๋ ํ๊ณ  ์์ผ๋ฉฐ,

Data๊ฐ ์๋ฐ์ดํธ๋๋ฉด์ ๋ณ๊ฒฝ๋ Data์ ๋ฐ๋ผ์ View์๋ค๊ฐ ๋ณ๊ฒฝ๋ Data๋ฅผ ๊ฐ๊ณต์์ผ์ View์ ๊ฝ์๋ฒ๋ฆฐ๋ค.

์ฌ์ฉ์๋ค์ด View์๋ค๊ฐ ์ตํฐ๋์์ผ๋ก ๋ฒํผ์ ํด๋ฆญํ๊ฒ ๋๋ฉด โํด๋ฆญ์ด ๋์์ด์โ๋ผ๊ณ  View Model์๊ฒ ์๋ ค์ค๋ค.

๊ทธ๋ฌ๋ฉด View Model์ ํด๋ฆญ์ ํ์ํ ๋น์ฆ๋์ค ๋ก์ง์ ํ์ํ ๋์์ ์ฐพ์์ ์์ฒญํ๋๋ก ํ ๊ฒ ์ผ๋จ์ ์ธํฐ๋์์ด ์์ผ๋ฉด ์๋ ค์ค ๋ผ๋ ์ญํ ์ ํ๋ค.

๊ทธ๋์ ํ๋์ ์ฝ๋๊ฐ์ฒด๊ฐ ๋๋ฌด ๋ง์ ์ฑ์์ ๊ฐ์ง๊ฒ ๋๋ ๊ฒ๋ณด๋ค ์ด ๊ฐ์ฒด๋ ํ๋์ ์ฑ์์ ์ง ์ ์๊ฒ๋ ํน์  ํจํด์ ์ ์ํ ๊ฒ์ ๋ง์ ๊ฐ๋ฐ์๋ค์ด ์ฑํํ ๊ฒ์ด ๋ฐ๋ก MVVM์ด๋ค. 

# ์ฝ๋๋ฅผ ์ ์ง๊ณ  ์ ์ง๋ณด์ ๊ฐ๋ฅํ๊ฒ๋ ๋ฏธ๋์ ์ฝ๋๋ฅผ ๋ณด๋ ์ฌ๋์ ์ํด์ ๋ฐฐ๋ คํ๋ ๋ง์์ผ๋ก ๋์์ธํจํด์ ๊ณต๋ถํ๋ ๊ฒ์ด๋ค.
