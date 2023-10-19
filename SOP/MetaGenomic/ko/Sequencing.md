
# I. Preparation for sequencing
## [1] Biological samples
1. 분변 채취용 키트 (NBG-4, Noble Biosciences)의 검채용 스푼과 스패츌러를 이용하여 fecal sample을 채취한 뒤 잘 흔들어 주어 검체를 균일하게 해준 뒤 -80℃에 보관한다. 


## [2.1] DNA preparation for short reads sequencing
### Reagents  
**FastDNA SPIN Kit for Feces (MP Biomedicals)**  
- Sodium Phosphate Buffer (MP Biomedicals), MT Buffer (MP Biomedicals), PLS Solution (MP Biomedicals), PPS Solution (MP Biomedicals), Wash Buffer #1(MP Biomedicals), Wash Buffer #2 (MP Biomedicals), TES (MP Biomedicals), 100% ethanol


### DNA extraction  
1. Fume hood에서 전자저울과 멸균된 스패츌러를 이용하여 아이스에 꽂아 둔 분변 샘플 500mg을 Lysing matrix E tube에 옮긴다. 
2. 825 μl의 sodium phosphate buffer와 825 μl의 PLS 솔루션을 넣고 뚜껑을 닫은 뒤 샘플이 튜브안에서 풀어지도록 10-15초간 vortexing 한다.
3. 샘플을 14,000ⅹg로 5분동안 원심분리 한 후 상층액을 버린다.
4. 978 μl의 sodium phosphate buffer와 122 μl의 MT buffer를 넣은 후 다시 샘플이 풀어질 때 까지 voltexing한다.
5. FastPrep 24 기기와 같은 beadbeater를 이용하여 6.0m/s 속도로 40초간 샘플을 파쇄 및 균질화 한다. (만약 크기가 큰 debris 때문에 파쇄가 충분하지 않았다고 판단되면,, 모든 샘플에 동일한 조건으로 추가 파쇄를 진행하되 진동 때문에 발생하는 열에 주의하며 충분히 interval을 두도록 한다.) 
6. 샘플을 14,000ⅹg로 5분동안 원심분리 한 후 상층액을 2ml tube로 옮긴다.
7. 250 μl의 PPS solution을 첨가한 뒤 천천히 inverting한 뒤 (vortexing 금지) 4℃에서 10분간 보관했다가 2분동안 14,000ⅹg로 원심분리 한다.
8. 원심분리 하는 동안 binding matrix solution 1 ml을 15 ml conical tube에 옮겨놓는다.
9. 원심분리가 끝난 샘플의 상층액을 binding matrix solution을 넣었던 15 ml tube에 옮기고 inverting한 다음 내용물이 충분히 섞일 수 있는 각도로 shaker에 3-5분동안 놔둔다.
10. Shaking incubator에 샘플이 충분히 잘 섞일 수 있는 각도로 tube를 꽂은 뒤 3-5분동안 놔둔다.
11. 2분동안 14,000ⅹg로 원심분리 한 후 상층액을 버린다.
12. 1 ml의 wash buffer #1을 넣고 부드럽게 pellet을 재현탁 한다.
13. SPIN filter tube에 binding matrix와 wash buffer #1 혼합액을 600 μl 옮긴 뒤 1분동안 14,000ⅹg로 원심분리 한 후 catch tube를 비운 뒤 다시 남은 용액을 옮겨 원심분리 한다. 이후 catch tube를 다시 비운다.
14. 500 μl의 wash buffer #2 (에탄올이 첨가된)를 SPIN filter tube에 넣고 부드럽게 pipetting 후 resuspension한다 (vortexing 금지).
15. 2분동안 14,000ⅹg로 원심분리 한 후 catch tube를 비운다.
16. 다시 2분동안 14,000ⅹg로 원심분리 한 하여 pellet에 남아있는 잔여 wash buffer를 날려 dry한 상태가 되도록 한다.
17. SPIN filter 버켓을 새 1.9 ml catch tube로 옮긴 뒤 60-100 μl의 TES 용액을 첨가한다. 손 끝을 이용하여 pellet이 용액과 섞이도록 tapping 한다. (vortexing 금지)
18. 2분동안 14,000ⅹg로 원심분리 하여 pellet에서 DNA를 elution한다. 
19. Nano drop을 이용하여 정량한 뒤 -20℃에 얼려서 보관한다.

## [2.2] DNA preparation for long reads seqencing
### Reagents
**QIAamp PowerFecal DNA kit (Qiagen)**  
(Long read 시퀀싱을 위해서 DNA 양이 많이 필요하며, DNA fragmentation을 최소화해야하기 때문에, PacBio사에서 추천하는 **QIAamp PowerFecal DNA kit** (Qiagen)를 사용하였다.)


### DNA extraction
키트 제조사의 프로토콜을 따라 분변으로부터 DNA extraction을 수행하였음.


