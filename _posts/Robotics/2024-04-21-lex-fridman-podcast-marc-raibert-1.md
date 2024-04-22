---
title: 번역 - Marc Raibert | Boston Dynamics and the Future of Robotics (Lex Fridman Podcast)
date: 2024-04-21
categories: [Robotics]
tags: [Robotics]
---

이 게시글은 Lex Fridman Podcast의 Script 내용과 이를 번역한 글입니다.

원본 영상:
[Marc Raibert: Boston Dynamics and the Future of Robotics | Lex Fridman Podcast #412](https://www.youtube.com/watch?v=5VnbBCm_ZyQ)

### Introduction

[1]

- So BigDog became LS3, which is the big load-carrying one.
- [Lex] Just a quick pause. It can carry 400 pounds.
- It was designed to carry 400, but we had it carrying about 1,000 pounds at one time.
- Of course you did, just to make sure.
- **We had one carrying the other one, we had two of them so we had one carrying the other one.**

[1-ko]

- 그래서 빅독은 LS3가 되었고 그것은 무거운 짐을 들 수 있죠.
- [Lex] 잠깐 살펴보죠. 400 파운드를 들 수 있네요.
- 400 파운드를 들도록 설계되었지만, 한 번에 1,000 파운드를 들 수 있었죠.
- 물론 그러셨지요, 혹시나 해서요.
- 하나가 다른 하나를 운반하고 있었고, 우리는 두 개를 가지고 있었기에 하나가 다른 하나를 운반하고 있었죠. (?)

[2]

- So one of the things that stands out about the robots Boston Dynamics have created is how beautiful the movement is, how natural the walking is, and running is even flipping when it's throwing so maybe you can talk about what's involved in making it look natural.
- [Marc] Well, I think having good hardware is part of the story, and people who think you don't need to innovate hardware anymore are wrong.

[2-ko]

- 그래서 보스턴 다이내믹스가 만든 로봇들의 눈에 띄는 점들 중 하나는 움직임이 얼마나 아름답고, 걸음이 얼마나 자연스러운지, 뛰는 것도 심지어 던지면서 뒤집히면서도요. 아마도 무엇이 그것을 자연스럽게 보이게 하는 데 무엇이 관련되어 있는지에 대해 이야기 해주실 수 있을 것 같아요.
- [Marc] 음, 저는 좋은 하드웨어가 그 이야기의 일부라고 생각하고, 더 이상 하드웨어의 발전이 필요하지 않다고 생각하는 사람들은 틀렸어요.

[3]

- The following is a conversation with Marc Raibert, a legendary roboticist founder and longtime CEO of Boston Dynamics and recently the executive director of the newly created Boston Dynamics AI Institute that focuses on research and the cutting edge on creating future generations of robots that are far better than anything that exists today.
  He has been leading the creation of incredible legged robots for over 40 years at CMU, at MIT, the legendary MIT Leg Lab, and then of course, Boston Dynamics with amazing robots like BigDog, Atlas, Spot and Handle.
  This was a big honor and pleasure for me.
  This is the Lex Fridman podcast. To support it, please check out our sponsors in the description. And now, dear friends, here's Marc Raibert.

[3-ko]

- 이후는 Marc Raibert와의 대화입니다. 그는 전설적인 로봇 공학자 창업자이자 오랜 기간 보스턴 다이내믹스의 CEO이자 최근에 새로 만들어진 보스턴 다이내믹스 AI 연구소의 전무 이사이죠. 해당 연구소는 오늘날 존재하는 것 보다 훨씬 나은 미래 세대의 로봇을 만드는 연구와 첨단 기술에 초점을 맞추고 있습니다.
  그는 CMU, MIT, 전설적인 MIT Leg 연구소, 그리고 물론 보스턴 다이내믹스에서 빅독, 아틀라스, 스팟, 핸들과 같은 놀라운 로봇들로 굉장한 다리 달린 로봇을 만드는 데 40년 이상을 이끌고 있습니다.
  이것은 저에게 큰 영광이고 기쁨이었습니다.
  이것은 Lex Fridman 팟캐스트입니다. 도움을 주시기위해서는, 설명에 있는 스폰서들을 확인해주세요. 그럼 이제, 친애하는 친구들, Marc Raibert 입니다.

### Early robots

[1]

- When did you first fall in love with the robotics?
- Well, I was always a builder from a young age.
  **I was lucky, my father was a frustrated engineer, and by that I mean he wanted to be an aerospace engineer, but his mom from the old country thought that that would be like a grease monkey and so she said no.**
  So he became an accountant. But the result of that was our basement was always full of tools and equipment and electronics.
  And, you know, from a young age, I would watch him assembling a kit, an Aiko kit or something like that.
  I still have a couple of his old Aiko kits.
  **But it was really during graduate school when I followed a professor back from class, it was Bertolt at MIT and I was taking an interim class.**
  It's IAP, Independent Activities Period.
  And I followed him back to his lab.
  And on the table was a vyke arm, robot arm taken apart in probably 1,000 pieces.
  And when I saw that, you know, from that day on, I was a roboticist.

[1-ko]

- 로봇과 처음 사랑에 빠진 때는 언제인가요?
- 음, 저는 어려서부터 언제나 빌더였죠.
  저는 운이 좋았죠. 저희 아버지는 좌절한 엔지니어였고, 그 말은 그가 항공우주 엔지니어가 되고 싶다는 것을 의미하지만, 오래된 나라의 그의 어머니는 그것이 그리스 원숭이 같을 것이라고 생각했고, 그래서 그녀는 안된다고 했습니다.
  그래서 그는 회계사가 되었어요. 하지만 그 결과로 저희 창고는 언제나 도구와 장비와 전자제품들도 가득 차있었죠.
  그리고, 아시다시피, 어릴 때 부터, 저는 그가 Aiko 키트나 다른 비슷한 키트를 조립하는 것을 지켜보곤 했지요.
  저는 아직 그의 오래된 Aiko 키트 몇 개를 가지고 있어요.
  하지만 제가 수업을 마치고 돌아가 교수님을 따라갔을 때는 대학원 과정 중이었고, MIT의 베르톨트 선생님이었고 중간(임시) 수업을 듣고 있었습니다.
  IAP, 독립 활동 기간입니다.
  그리고 저는 그를 따라 그의 연구실로 돌아갔습니다.
  그리고 테이블에는 바이크 팔이 있었는데 아마 1,000 조각 정도로 분해된 로봇팔이었습니다.
  그리고 그걸 봤을 때, 그 날부터 저는 로봇공학자였습니다.

[2]

- Do you remember the year?
- [Marc] 1974.
- 1974. So there's just this arm in pieces.
- [Marc] Yeah.
- And you saw the pieces and you saw in your vision, the arm when it's put back together and the possibilities that holds.
- Somehow it spurred my imagination.

[2-ko]

- 그 년도를 기억하시나요?
- [Marc] 1974년.
- 1974년. 그러니까 거기 그냥 팔이 조각나 있구요.
- [Marc] 네.
- 그리고 당신은 그 조각들을 보았고 당신의 비전에서 그 팔이 다시 조립됐을 때와 그것이 유지되는 가능성을 보았군요.
