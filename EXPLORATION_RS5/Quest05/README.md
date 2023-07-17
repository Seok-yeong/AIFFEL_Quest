# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김석영
- 리뷰어 : 서희원


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.
- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?

- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네 코드별로 주석을 작성해주셔서 잘 이해했습니다.
  ```python
  # 이미지 색상 채널을 변경해야함 (BGR 형식을 RGB 형식으로 변경) 
  img_mask_color = cv2.cvtColor(img_mask, cv2.COLOR_GRAY2BGR)
  
  # 이미지 반전
  img_bg_mask = cv2.bitwise_not(img_mask_color)
  
  # cv2.bitwise_and()을 사용해 배경만 있는 이미지 추출
  img_bg_blur = cv2.bitwise_and(img_orig_blur, img_bg_mask)
  plt.imshow(cv2.cvtColor(img_bg_blur, cv2.COLOR_BGR2RGB))
  plt.show()
  ```
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 네 출력결과가 다 나와있어 에러가 나지 않고 잘 작동하는 것을 알 수 있습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네 중각 과정과정을 출력하면서 잘이해하고 있는 것 같습니다.
- [X] 코드가 간결한가요?
  > 네 기능별로 구분해 한눈에 보기 쉽습니다.
  ```python
  # 이미지 색상 채널을 변경해야함 (BGR 형식을 RGB 형식으로 변경) 
  # 세그멘테이션 마스크가 255인 부분만 원본 이미지 값 가져옴
  img_concat = np.where(img_mask_color==255, img_orig, img_bg_blur)
  
  # 이미지 색상 채널 변경(BGR 형식을 RGB 형식으로 변경)
  plt.imshow(cv2.cvtColor(img_concat, cv2.COLOR_BGR2RGB))
  plt.show()
  ```
# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python

```

# 참고 링크 및 코드 개선
```python

```
