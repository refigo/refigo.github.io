---
title: 번역 - Marc Raibert | Boston Dynamics and the Future of Robotics (Lex Fridman Podcast)
date: 2024-04-21
categories: [Robotics]
tags: [Robotics]
---

이 게시글은 Lex Fridman Podcast의 Script 내용과 이를 번역한 글입니다.

원본 영상:
[Marc Raibert: Boston Dynamics and the Future of Robotics | Lex Fridman Podcast #412](https://www.youtube.com/watch?v=5VnbBCm_ZyQ)

## Introduction

[1]

- So BigDog became LS3, which is the big load-carrying one.
- [Lex] Just a quick pause. It can carry 400 pounds.
- It was designed to carry 400, but we had it carrying about 1,000 pounds at one time.
- Of course you did, just to make sure.
- **We had one carrying the other one, we had two of them so we had one carrying the other one.**

- 그래서 빅독은 LS3가 되었고 그것은 무거운 짐을 들 수 있죠.
- [Lex] 잠깐 살펴보죠. 400 파운드를 들 수 있네요.
- 400 파운드를 들도록 설계되었지만, 한 번에 1,000 파운드를 들 수 있었죠.
- 물론 그러셨지요, 혹시나 해서요.
- 하나가 다른 하나를 운반하고 있었고, 우리는 두 개를 가지고 있었기에 하나가 다른 하나를 운반하고 있었죠. (?)

[2]

- So one of the things that stands out about the robots Boston Dynamics have created is how beautiful the movement is, how natural the walking is, and running is even flipping when it's throwing so maybe you can talk about what's involved in making it look natural.
- [Marc] Well, I think having good hardware is part of the story, and people who think you don't need to innovate hardware anymore are wrong.

- 그래서 보스턴 다이내믹스가 만든 로봇들의 눈에 띄는 점들 중 하나는 움직임이 얼마나 아름답고, 걸음이 얼마나 자연스러운지, 뛰는 것도 심지어 던지면서 뒤집히면서도요. 아마도 무엇이 그것을 자연스럽게 보이게 하는 데 무엇이 관련되어 있는지에 대해 이야기 해주실 수 있을 것 같아요.
- [Marc] 음, 저는 좋은 하드웨어가 그 이야기의 일부라고 생각하고, 더 이상 하드웨어의 발전이 필요하지 않다고 생각하는 사람들은 틀렸어요.

[3]

- The following is a conversation with Marc Raibert, a legendary roboticist founder and longtime CEO of Boston Dynamics and recently the executive director of the newly created Boston Dynamics AI Institute that focuses on research and the cutting edge on creating future generations of robots that are far better than anything that exists today.
  He has been leading the creation of incredible legged robots for over 40 years at CMU, at MIT, the legendary MIT Leg Lab, and then of course, Boston Dynamics with amazing robots like BigDog, Atlas, Spot and Handle.
  This was a big honor and pleasure for me.
  This is the Lex Fridman podcast. To support it, please check out our sponsors in the description. And now, dear friends, here's Marc Raibert.

- 이후는 Marc Raibert와의 대화입니다. 그는 전설적인 로봇 공학자 창업자이자 오랜 기간 보스턴 다이내믹스의 CEO이자 최근에 새로 만들어진 보스턴 다이내믹스 AI 연구소의 전무 이사이죠. 해당 연구소는 오늘날 존재하는 것 보다 훨씬 나은 미래 세대의 로봇을 만드는 연구와 첨단 기술에 초점을 맞추고 있습니다.
  그는 CMU, MIT, 전설적인 MIT Leg 연구소, 그리고 물론 보스턴 다이내믹스에서 빅독, 아틀라스, 스팟, 핸들과 같은 놀라운 로봇들로 굉장한 다리 달린 로봇을 만드는 데 40년 이상을 이끌고 있습니다.
  이것은 저에게 큰 영광이고 기쁨이었습니다.
  이것은 Lex Fridman 팟캐스트입니다. 도움을 주시기위해서는, 설명에 있는 스폰서들을 확인해주세요. 그럼 이제, 친애하는 친구들, Marc Raibert 입니다.

## Early robots

[1 - 1:43 ~ 2:58]

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

- 로봇과 처음 사랑에 빠진 때는 언제인가요?
- 음, 저는 어려서부터 언제나 빌더였죠.
  저는 운이 좋았죠. 저희 아버지는 좌절한 엔지니어였고, 그 말은 그가 항공우주 엔지니어가 되고 싶다는 것을 의미하지만, 오래된 나라의 그의 어머니는 그것이 그리스 원숭이 같을 것이라고 생각했고, 그래서 그녀는 안된다고 했습니다.
  그래서 그는 회계사가 되었어요. 하지만 그 결과로 저희 창고는 언제나 도구와 장비와 전자제품들도 가득 차있었죠.
  그리고, 아시다시피, 어릴 때 부터, 저는 그가 Aiko 키트나 다른 비슷한 키트를 조립하는 것을 지켜보곤 했지요.
  저는 아직 그의 오래된 Aiko 키트 몇 개를 가지고 있어요.
  하지만 제가 수업을 마치고 돌아가 교수님을 따라갔을 때는 대학원 과정 중이었고, MIT의 베르톨트 선생님이었고 중간(임시) 수업을 듣고 있었습니다.
  IAP, 독립 활동 기간입니다.
  그리고 저는 그를 따라 그의 연구실로 돌아갔습니다.
  그리고 테이블에는 바이크 팔이 있었는데 아마 1,000 조각 정도로 분해된 로봇팔이었습니다.
  그리고 그걸 봤을 때, 그 날부터 저는 로봇공학자였습니다.

[2 - 2:59 ~ 3:58]

- Do you remember the year?
- [Marc] 1974.
- 1974. So there's just this arm in pieces.
- [Marc] Yeah.
- And you saw the pieces and you saw in your vision, the arm when it's put back together and the possibilities that holds.
- Somehow it spurred my imagination.
  I was in the brain and cognitive sciences department as a graduate student doing neurophysiology.
  I'd been an electrical engineer as an undergrad at Northeastern.
  And the neurophysiology wasn't really working for me.
  You know, it wasn't conceptual enough.
  **I couldn't see really how by looking at single neurons, you were gonna get to a place where you could understand, you know, control systems or thought or anything like that.**
  And, you know, the AI lab was always an appealing, this was before C-SAIL right?
  This was in the '70s so the AI lab was always an appealing idea.
  And so when I went back to the AI lab following him and I saw the arm, I just thought, you know, this is it.

- 그 년도를 기억하시나요?
- [Marc] 1974년.
- 1974년. 그러니까 거기 그냥 팔이 조각나 있구요.
- [Marc] 네.
- 그리고 당신은 그 조각들을 보았고 당신의 비전에서 그 팔이 다시 조립됐을 때와 그것이 유지되는 가능성을 보았군요.
- 어쩐지 그게 내 상상력을 자극했어요.
  저는 대학원생으로 뇌 인지 과학과에서 신경생리학을 공부하고 있었죠.
  저는 Northeastern에서 학부생으로 전기 기술자로 일했습니다.
  그리고 신경생리학은 저에게 실제 효과가 없었어요.
  알다시피, 그것은 개념적으로 충분하지 않았습니다.
  단일 뉴런을 관찰함으로써 어떻게 제어 시스템이나 생각 등을 이해할 수 있는 지점에 도달할 수 있는지 알 수 없었습니다.
  그리고 아시다시피 AI 연구실은 언제나 매력적이었습니다. C-SAIL 이전이었지요?
  당시는 70년대였기 때문에 AI 연구실은 항상 매력적인 아이디어였습니다.
  그래서 그를 따라 AI 연구실로 들어가서 팔을 봤을 때, 저는 그렇게 생각했죠, 그게 다에요.

[3 - 3:59 ~ 4:47]

- It's so interesting the tension between the BCS, brain cognitive science approach to understanding intelligence and the robotics approach to understanding intelligence.
- Well, BCS is now morphed a bit, right?
  They have the Center for Brains, Minds and Machines, which is trying to bridge that gap.
  And even when I was there, you know, David Maher was in the AI lab.
  David Maher had models of the brain that were appealing both to biologists, but also to computer people.
  So he was a visitor in the AI lab at the time, and I guess he became full-time there.
  So that was the first time a bridge was made between those two groups.
  Then the bridge kind of went away and then there was another time in the '80s.
  And then recently, you know, the last five or so years, there's been a stronger connection.

- 지능을 이해하기 위한 뇌 인지 과학 접근 방식인 BCS와 지능을 이해하기 위한 로봇 공학 접근 방식 사이의 긴장이 매우 흥미롭네요.
- 음, BCS는 이제 조금 변형됐죠?
  그들은 그 격차를 해소하기 위해 노력하는 두뇌, 정신 및 기계 센터를 보유하고 있습니다.
  제가 그곳에 있을 때도, David Maher는 AI 연구실에 있었습니다.
  David Maher는 생물학자 뿐만 아니라 컴퓨터 사람들에게도 매력적인 뇌 모델을 가지고 있었습니다.
  그래서 그는 그 당시 AI 연구실의 방문자였고, 그곳에서 정규직이 된 것 같아요.
  그래서 두 그룹 사이에 첫 번째 다리가 만들어졌습니다.
  그런 다음 다리가 사라지고 80년대에 또 다른 시기가 있었습니다.
  그리고 최근, 지난 5년 정도 동안 더욱 강력한 연결이 이루어졌습니다.

[4 - 4:48 ~ 5:26]

- You said you were always kind of a builder.
  What stands out to you in memory of a thing you've built?
  Maybe a trivial thing that just kind of like inspired, inspired you in the possibilities that this direction of work might hold?

- 당신은 항상 빌더였다고 하셨죠.
  당신이 만든 것 중 기억에 남는 것은 무엇인가요?
  아마도 영감을 받은 사소한 일이 이 작업 방향이 가질 수 있는 가능성에 대해 영감을 주었을까요?

- I mean, we were just doing gadgets when we were kids.
  I have a friend, we were taking, you know the... I don't know if everybody remembers, but fluorescent lights had this little aluminum cylinder, I can't even remember what it's called now, that you needed a starter, I think it was.
  And we would take those apart, fill 'em with match heads, put a tail on it, and make it into little rockets.

- 내 말은, 우리는 어렸을 때 그저 도구를 만들고 있었을 뿐이라는 거죠.
  저의 한 친구가 있어요, 우리가 가져간게 있는데... 모두가 기억할지 모르겠지만, 형광등에는 이 작은 알루미늄 원통이 있었는데, 지금은 그것을 뭐라고 부르는지 조차 기억나지 않는데요, 스타터가 필요하댔던 것 같아요.
  그리고 우리는 그것을 분해해서, 성냥개비로 채우고, 그 위에 꼬리를 달고, 작은 로켓을 만들었습니다.

[5 - 5:27 ~ 6:46]

- So it wasn't always about function, it was-
- [Marc] Well, a rocket was pretty much function.
- I guess that is pretty functional.
  But yeah, I guess that is a question.
  How much was it about function versus just creating something cool?

- 항상 기능에 관한 것은 아니었군요.
- [Marc] 음, 로켓은 거의 기능에 관한 것이었습니다. ㅋㅋㅋ
- 꽤 기능적인 것 같아요. ㅋㅋㅋㅋ
  하지만 네, 그게 질문인 것 같아요.
  멋진 것을 만드는 것보다 기능에 더 중점을 두었나요?

- I think it's still a balance between those two.
  There was a time though, when I was, I guess I was probably already a professor or maybe late in graduate school when I thought that function was everything.
  **And that, you know, mobility, dexterity, perception and intelligence, those are sort of the key functionalities for robotics, that that's what mattered and nothing else mattered.**
  And I even had kind of this platonic ideal that a robot, if you just looked at a robot and it wasn't doing anything, it would look like a pile of junk, which a lot of my robots looked like in those days.
  But then when it started moving, you'd get the idea that it had some kind of life or some kind of interest in its movement.
  And I think we purposely even designed the machines, not worrying about the aesthetics of the structure itself.
  But then you know, it turns out that the aesthetics of the thing itself add and combine with the lifelike things that the robots can do.
  But the heart of it is, you know, making them do things that are interesting.

- 아직은 둘 사이의 균형이 맞는 것 같아요.
  하지만 제가 이미 교수가 되었거나 대학원에 늦게 입학했을 때 기능이 전부라고 생각했던 때가 있었습니다.
  그리고 아시다시피 이동성, 민첩성, 지각 및 지능은 로봇 공학의 핵심 기능이며, 그것이 중요하고 다른 것은 중요하지 않습니다.
  그리고 저는 아무 일도 하지 않는 로봇을 보면 쓰레기 더미 처럼 보일 것이라는 로봇에 대한 플라토닉한 이상을 갖고 있었습니다. 그 당시 제가 만든 많은 로봇은 그런 모습이었습니다.
  그러나 그것이 움직이기 시작하면, 그것이 어떤 종류의 생명을 갖고 있거나 그 움직임에 어떤 종류의 관심을 가지고 있다는 생각을 갖게 될 것입니다.
  그리고 우리는 구조 자체의 미적인 측면을 고려하지 않고 의도적으로 기계를 설계했다고 생각해요.
  하지만 알고 보면, 사물 자체의 미학이 로봇이 할 수 있는 생명체와 같은 일과 더해지고 결합된다는 사실이 밝혀지죠.
  하지만 그것의 핵심은, 아시다시피, 그들이 흥미로운 일을 하도록 만드는 것입니다.

## AI Institute

[1 - 51:23 ~ 51:56]

- [Lex] So this might be a good place to mention that you're now leading up the Boston Dynamics AI Institute newly formed, which is focused more on designing the robots of the future.
  I think one of the things, maybe you can tell me the big vision for what's going on, but one of the things is this idea that hardware still matters with organic design and so on.
  Maybe before that, can you zoom out and tell me what the vision is for the AI Institute?

- [Lex] 그래서 지금이 아마 이번에 새로 설립된 보스턴 다이내믹스 AI 연구소(Boston Dynamics AI Institute)를 이끌고 계시다는 점을 언급하기 좋은 때인 것 같아요. 미래의 로봇 설계에 더 중점을 두고 있는 곳 말이죠.
  제 생각에는 무슨 일이 일어나고 있는지에 대한 큰 비전을 말해 주실 수 있을 것 같지만, 그 중 하나는 하드웨어가 여전히 유기적 디자인 등에 중요하다는 생각입니다.
  어쩌면 그 전에, AI 연구소의 비전이 무엇인지 말씀해 주시겠습니까?

## Optimus robot

[1 - 1:25:33 ~ 1:27:12]

- Let me ask you about some competitors.
- [Marc] Sure.
- You've been complimentary of Elon and Tesla's work on Optimus Robot with their humanoid robot.
  What do you think of their efforts there with the humanoid robot?

- 몇몇 경쟁 업체들에 대해 물어보겠습니다.
- [Marc] 물론이죠.
- 당신은 휴머노이드 로봇을 이용한 Optimus Robot에 대한 Elon과 Tesla의 작업에 찬사를 보냈습니다.
  그들의 노력에 대해 어떻게 생각하시나요?

- You know, I really admire Elon as a technologist.
  I think that what he did with Tesla, it was just totally mind boggling that he could go from this totally niche area that less than 1% of anybody seemed to be interested to making it so that essentially every car company in the world is trying to do what he's done so you gotta give it to him.
  Then look at SpaceX, you know, he's basically replaced NASA if you could, that might be a little exaggeration, but not by much.
  So you gotta admire the guy and I wouldn't count him out for anything.
  I don't think Optimus is today is where Atlas is, for instance.
  I don't know, it's a little hard to compare 'em to the other companies.
  You know, I visited Figure.
  I think they're doing well and they have a good team.
  I've visited Apptronik and I think they have a good team and they're doing well.
  But Elon has a lot of resources.
  He has a lot of ambition.
  I'd like to take some credit for his ambition, I think.
  I think if I read between the lines, it's hard not to think that him seeing what Atlas is doing is a little bit of an inspiration.
  I hope so.

- 아시다시피, 저는 Elon을 기술자로서 정말 존경합니다.
  내 생각에 그가 Tesla에서 한 일은 정말 놀라운데요. 1% 미만만이 갈 수 있는 틈새시장에서 갈 수 있다는 것이요. 본질적으로 세계의 모든 자동차 회사가 하고자 노력하고 있는 것을 그가 해왔고 그가 성취해야한다고 봐요.
  SpaceX를 봐요, 아시다시피, 그는 기본적으로 NASA를 대체했어요. 약간 과장일 수 있지만 그리 심하지 않다고 생각해요.
  그러니 그를 존경해야하고 저는 그를 어떤 이유로도 배제하지 않을 겁니다.
  예를들어, 저는 오늘날 Optimus가 Atlas와 같은 포지션에 있다고 생각하지 않습니다.
  다른 회사와 비교하기는 좀 어렵네요.
  알다시피, 저는 Figure에 방문했습니다.
  저는 그들이 잘하고 있고 좋은 팀을 가지고 있다고 생각합니다.
  Apptronik을 방문했는데 좋은 팀이 있고 잘 하고 있는 것 같아요.
  하지만 Elon은 많은 자원을 가지고 있습니다.
  그는 야망이 많습니다.
  저는 그의 야망에 대해 어느 정도 공로를 인정하고 싶다고 생각합니다.
  어떤 의미냐면, 그가 Atlas가 하고 있는 일을 보는 것이 저에게 약간의 영감을 준다고 생각하지 않을 수 없을 것 같습니다.
  저는 그러길 희망해요.
