# Jetson-nano
<details>
    <summary>이미지 보기</summary>
    
![jetson-nano-dev-kit-top-r6-HR-B01](https://github.com/user-attachments/assets/b713300c-4429-41c0-9474-7b443e2ebee0)

</details>

# 준비하는 과정

### 1. SD Card Formatter 다운로드
https://sd-memory-card-formatter.en.softonic.com/download

### 2. jet pack 다운로드
https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write

### 3. 계정 설정

### 4. Ubuntu 한글 입력기 설치
https://driz2le.tistory.com/253
<details>
    <summary>자세히</summary>

1) 크롬 띄우고 링크로 가기
![Screenshot from 2024-11-14 20-22-09](https://github.com/user-attachments/assets/c40c4a0d-11b1-4ba0-8725-045627dd0523)
2) ![Screenshot from 2024-11-14 21-04-02](https://github.com/user-attachments/assets/89fc8d97-158b-4114-94c9-9307cacad79c) Terminal에서 $ sudo apt-get update 입력
![Screenshot from 2024-11-14 20-23-15](https://github.com/user-attachments/assets/462a36a6-fb4d-40f0-a22b-522b2685fa70)
3) $ sudo apt-get install fcitx-hangul 입력
![Screenshot from 2024-11-14 20-23-56](https://github.com/user-attachments/assets/eec33d31-6e69-459f-8dd3-ff251b1d42a8)
4) ![Screenshot from 2024-11-14 21-07-55](https://github.com/user-attachments/assets/cdf047c3-bfaa-4f71-9d54-e313b230ba82)설정 에서 ![Screenshot from 2024-11-14 21-08-43](https://github.com/user-attachments/assets/da96f2ea-a031-494b-8305-ad6260948aa5) Language Support 들어가기
![Screenshot from 2024-11-14 20-27-22](https://github.com/user-attachments/assets/4aec7b4d-634c-4618-9b40-fd780dbd9ddc)
5) 하단 Keyboard input method system 설정을 fcitx로 바꾼다.
![Screenshot from 2024-11-14 20-36-17](https://github.com/user-attachments/assets/751b3b9f-fb13-4056-9b7c-a32fd4106976)

6) 재부팅
7) 하단 + 누르고 hangul 찾기
![Screenshot from 2024-11-14 20-37-38](https://github.com/user-attachments/assets/3a7d3bc0-7905-490f-aece-15f61856f97d)
![Screenshot from 2024-11-14 20-38-33](https://github.com/user-attachments/assets/5fdef70c-09e0-4a0f-8d53-d249796bb26f)
8) 공백칸 누르고 '한/영'키 입력
![Screenshot from 2024-11-14 20-39-23](https://github.com/user-attachments/assets/a5616675-0150-4d1d-9e25-798ebb86021e)

</details>

# 실습

## 카메라 인식

<details>
    <summary>자세히</summary>

![Screenshot from 2024-11-14 20-53-18](https://github.com/user-attachments/assets/c8e194bf-1b46-4e40-85a3-4b1deca71734)


![Screenshot from 2024-11-14 20-52-20](https://github.com/user-attachments/assets/28629904-0613-4bf0-b256-a82fac056ab1)

</details>

## 헤드리스모드

<details>
    <summary>자세히</summary>
    
1) 교육과정에 필요한 dir 추가하기

    ~$ mkdir -p ~/nvdli-data

    ~$ ls

2) Terminal 창에 입력
   
    sudo docker run --runtime nvidia -it --rm --network host \
    --memory=500M --memory-swap=4G \
    --volume ~/nvdli-data:/nvdli-nano/data \
    --volume /tmp/argus_socket:/tmp/argus_socket \
    --device /dev/video0 \
    nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1kr
![Screenshot from 2024-11-14 21-30-33](https://github.com/user-attachments/assets/d36251a2-67c8-409c-bde9-a5038aee8b57)

4) allow 10 sec for JupyterLab to start @ http://192.168.176.16:8888 (password dlinano)
JupterLab logging location:  /var/log/jupyter.log  (inside the container)
root@ai-desktop:/nvdli-nano# 

    ![Screenshot from 2024-11-14 21-38-48](https://github.com/user-attachments/assets/3e03b97b-a22a-4847-b886-8616ea187a0f)

5) Terminal에 아래 내용 입력하기
 
    sudo systemctl disable nvzramconfig
   
    sudo systemctl set-default multi-user.target
    sudo fallocate -l 18G /mnt/18GB.swap

    sudo chmod 600 /mnt/18GB.swap
    sudo mkswap /mnt/18GB.swap

    sudo su
    echo "/mnt/18GB.swap swap swap defaults 0 0" >> /etc/fstab    
    exit

    sudo reboot


5) 입력하고 리부트 후 아이디 비밀번호 입력한 뒤 시스템 GUI모드로 설정:

    sudo systemctl set-default graphical.target

    reboot  입력

![20241121_195357 (1)](https://github.com/user-attachments/assets/6e58f474-4763-472a-9214-09ef7149a68e)

</details>

## 이미지 학습시키기

<details>
    <summary>자세히</summary>
    
1) ![Screenshot from 2024-11-21 19-58-41](https://github.com/user-attachments/assets/5cabddfa-9ae4-43d9-b094-fb7c60de1b55)

2) ![Screenshot from 2024-11-21 19-59-32](https://github.com/user-attachments/assets/447d1d79-57c7-4dc0-ab31-396a4ee99f91)

3) ![Screenshot from 2024-11-21 20-00-49](https://github.com/user-attachments/assets/365ecb99-9465-4529-97b6-a7952930ea4d)![Screenshot from 2024-11-21 20-01-09](https://github.com/user-attachments/assets/5d48f834-a9ae-4d65-95f2-4ab7af9c0e7b)

4) 실행시키기
 
    ![Screenshot from 2024-11-21 20-01-55](https://github.com/user-attachments/assets/bcd37c99-2fbe-4a37-bdb4-7028991dc276)

5) add 버튼으로 데이터 셋 A에만 tumbs_up 30개, tumbs_down 30개, epochs 10으로 Train 시켜본다.

   ![Screenshot from 2024-11-21 20-09-31](https://github.com/user-attachments/assets/f0f6bad7-ec2e-4276-a1cd-805ea990a8a7)![Screenshot from 2024-11-21 20-17-10](https://github.com/user-attachments/assets/3e513705-6490-4b5d-8b7b-6a0991ae086b)![Screenshot from 2024-11-21 20-18-52](https://github.com/user-attachments/assets/855358a6-a7f1-455a-b6c8-f678b77216f8)![Screenshot from 2024-11-21 20-22-43](https://github.com/user-attachments/assets/bd9c4434-f853-4ba3-9a2e-79a473ac4e4c)


</details>
