# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 최한준
- 리뷰어 : 김석영


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네. 모든 코드가 정상적으로 작동하며,
  > 세 가지 평가문항 모두에 대해서도 상세기준에 부합하게 문제를 해결했습니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네. Task별로 상세하게 주석이 달려 있어서 이해에 전혀 무리가 없습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 작성된 코드 기준으로는 에러 유발 가능성은 보이지 않습니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네. Task의 수행 전 과정에 대해 주석이 상세히 작성돼 있고, 노드 학습에서 다루지 않은 코드들도 사용이 돼 있으므로, 충분한 이해를 바탕으로 작성이 됐다 할 수 있습니다.
- [O] 코드가 간결한가요?
  > 네. 중복된 코드의 사용 비율이 매우 낮고, 전체적으로 간결한 방식으로 코드가 작성이 됐습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 기울기 계산
top_nose = np.array(list_landmarks[0][27])
bottom_nose = np.array(list_landmarks[0][33])
slope = top_nose / bottom_nose

# sticker 회전 각도 계산
angle = np.arctan(slope[1] / slope[0]) * 180 / np.pi

# sticker 회전
print(cat_img_sticker.shape, "회전 후")
rotated_sticker = cv2.rotate(cat_img_sticker, cv2.ROTATE_90_COUNTERCLOCKWISE)
rotated_sticker = cv2.rotate(rotated_sticker, cv2.ROTATE_90_COUNTERCLOCKWISE)
print(rotated_sticker.shape, "회전 전")

# 이후에 사실 각도만큼 affine transform을 해야할 듯 하나, 이건 직접적으로 계산의 영역이 될 듯 해 생략함.

# 이미지 크기에 맞게 sticker 크기 조절
sticker_width = int(img_show.shape[1] * 0.25)
sticker_height = int(rotated_sticker.shape[0] * sticker_width / rotated_sticker.shape[1])
resized_sticker = cv2.resize(rotated_sticker, (sticker_width, sticker_height))

# sticker 중심 좌표 계산
center_x = int(img_show.shape[1] * 0.5)
center_y = int(img_show.shape[0] * 0.5)

# sticker를 이미지에 붙일 위치 계산
x = center_x - int(resized_sticker.shape[1] / 2)
y = center_y - int(resized_sticker.shape[0] / 2)


result = img_show.copy()
img_show[y - (rotated_sticker.shape[0] - 1) // 2: y + rotated_sticker.shape[0] // 2 + 1,
         x - (rotated_sticker.shape[1] - 1) // 2: x + rotated_sticker.shape[1] // 2 + 1] = \
          np.where(rotated_sticker==255,sticker_area,rotated_sticker).astype(np.uint8)

# 결과 이미지 출력
plt.imshow(result/255.0)
```

# 참고 링크 및 코드 개선
```python
회전 전과 회전 후의 결과가 다르게 보일 수 있는 경우의 image를 사용하면 더 좋을 거 같습니다.
```
