# 🔧 Lens Focus Control System

## 📘 프로젝트 소개
3채널 카메라 영상을 동시에 Grab하고, 시리얼 통신 기반의 버튼 입력으로 각 카메라의 렌즈 포커스를 제어하는 프로그램입니다.  
카메라 및 렌즈 정보를 Recipe로 관리하여 설정값을 쉽게 불러올 수 있으며, 지정된 경로와 이름으로 자동 저장 기능을 제공합니다.

---

## 🧰 기술 스택
- **Language**: C# (WinForms)  
- **SDK**: HikCamera SDK, Lens Connect SDK
- **Framework**: .NET Framework 4.8

---

## ⚙️ 주요 기능
- 3채널 카메라 영상 동시 출력  
- SerialPort 기반 버튼 입력을 통한 카메라별 렌즈 포커스 제어  
- Recipe 기능 (카메라, 렌즈 SerialNumber, Focus 값 등 저장)  
- Recipe에 지정된 파일 경로 및 TextBox 입력 이름 기반 자동 저장  

---

## 💼 수행 업무
- 3채널 카메라 영상 출력 기능 구현  
- SerialPort 기반 버튼 입력 및 포커스 제어 로직 구현  
- Recipe 구조 설계 및 파일 입출력 기능 구현  
- 지정 경로/이름 기반 이미지 자동 저장 기능 개발  

---

## 🧩 프로젝트 구조
```markdown
LensFocusControl/
├── Device/
│ ├── CameraManager.cs
│ ├── LensController.cs
│ └── SerialButton.cs
├── Process/
│ ├── FocusProcess.cs
│ └── RecipeManager.cs
├── UI/
│ ├── MainForm.cs
│ ├── WaitDialog.cs
│ └── ConfigForm.cs
└── Wrapper/
└── HikCameraWrapper.dll
```

## 🧠 프로젝트 회고
개발 환경에서는 **CogDisplay 컨트롤**이 정상적으로 생성되었으나, 실제 구동 PC에서는 **Display 생성에 약 2분**이 소요되는 문제가 발생했습니다.  
이는 Windows 10 환경에서 **Cognex VisionPro 라이브러리의 호환성 문제**로 확인되었으며, 다른 Display 컨트롤로 교체하여 로딩 속도를 크게 개선하였습니다.

렌즈 포커스 이동이 되지 않는 문제가 있었습니다.
원인을 분석해보니 세 렌즈가 동시에 구동 명령을 받아 충돌이 발생하는 것이 원인이었습니다.
이를 해결하기 위해 렌즈를 **순차적으로 이동하는 방식**으로 변경하였으며,
모든 렌즈의 이동이 완료될 때까지 사용자가 대기 상태를 인지할 수 있도록 Wait 창을 표시하여 UX를 개선했습니다.

유지보수성과 확장성을 위해 **카메라, 렌즈 포커스, 버튼 입력, 포트 관리 로직을 클래스 단위로 분리**하고,  
제조사 SDK를 **재가공한 Wrapper DLL** 형태로 구성하여 개발 편의성을 높였습니다.

---

## 🖼️ 프로그램 UI
