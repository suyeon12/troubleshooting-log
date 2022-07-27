virtualbox를 실행하려는데 다음과 같은 오류가 발생했다.

`Not in a hypervisor partition (HVP=0) (VERR_NEM_NOT_AVAILABLE). AMD-V is disabled in the BIOS (or by the host OS) (VERR_SVM_DISABLED).`



오류는 다음 링크를 참고하여 수정하였다.

[[Fix] Not in a hypervisor partition (HVP=0) (VERR_NEM_NOT_AVAILABLE) or VT-x is disabled in the BIOS for all CPU modes (VERR_VMX_MSR_ALL_VMX_DISABLED)](https://techsupportwhale.com/not-in-a-hypervisor-partition/)

[How to solve Oracle VM VirtualBox error with AMD Processors: AMD-V is disabled in the BIOS (or by the host OS) (VERR_SVM_DISABLED) | Our Code World](https://ourcodeworld.com/articles/read/1282/how-to-solve-oracle-vm-virtualbox-error-with-amd-processors-amd-v-is-disabled-in-the-bios-or-by-the-host-os-verr-svm-disabled)





1. 가상화 모드를 비활성화에서 활성화로 바꾸기

난 이미 활성화되어 있어서 별 도움이 되지는 않았다



2. Hyper-V 활성화를 비활성화로 바꾸기

마찬가지로 이미 비활성화 되어서 별 도움이 되지는 않았다



3. BIOS 모드에 접근해서 SVM 모드를 활성화로 바꾸기

여기서 차이점이 발견되었다!!

일단 BIOS 모드에 접근하는 법은 제조사마다 다른데 나는 `msi` 이기 때문에 다시 시작되는 동안 `del`키를 연타했다(...)  사실 화면에 보이는 깔끔한 BIOS가 아니라 체감상 왼쪽의 40%만 보이는 잘린 화면만 나왔는데 어떻게 SVM 모드를 찾을 수는 있었다.

나는 `Overclocking` 메뉴를 선택한 후 `CPU` 관련을 하나하나 눌러봤는데 그 중 `SVM Mode`를 발견할 수 있었다. 여기서 비활성화를 활성화로 바꿔준다.

이후가 난관이었는데 ESC로 나가니 알림창으로 '저장하지 않..'이 떴다. 이 뒤는 안 보여서 확신할 수는 없으나 딱 봐도 저장하지 않고 나가시겠습니까? 이런 알림이었을 것이라 예상한다. 왜냐면 아니오를 누르면 부팅이 안 되었으니까 ^^.. 여기서 변경 사항을 저장하려면 단축키 `F10` 을 누르면 된다!! ^ㅡ^



이후 virtualbox가 정상적으로 작동되었다.
