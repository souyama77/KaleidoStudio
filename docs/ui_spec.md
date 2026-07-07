# UIデザイン設計書 - Kaleido Studio

## 1. 本書の役割

本書は、Figma画像だけでは判断しにくいUI寸法・配置・表示ルールを定義する。
デザイン実装時の基準値のみ扱う。

---

## 2. 対象画面

| 画面             | 対象                                       |
| -------------- | ---------------------------------------- |
| Title          | 初期表示 / 認証Modal表示                         |
| Main Screen    | 描画画面 / Right Inspector表示                 |
| Auth Modal     | Login / CreateNewAccount / ResetPassword |
| UserName Modal | ユーザー名設定                                  |

---

## 3. 共通寸法

| 項目           |         値 |
| ------------- | ---------: |
| Desktop Frame | 1280 x 832 |
| Header Height |       56px |
| Base Grid     |        8px |
| Button Height |       48px |
| Button width  |      480px |
| Icon Button   |  48 x 48px |
| Border Radius |   12〜16px |
| Modal Width   |      653px |
| Modal Height  |      562px |
| Modal Padding |       32px |

---

## 4. 共通カラー

| 用途        | 基準値      |
| ----------- | --------- |
| Background  | #F7F8FA |
| Surface     | #FFFFFF |
| Surface Sub | #F1F3F5 |
| Text Main   | #0B1220 |
| Text Sub    | #667085 |
| Border      | #E3E7EE |
| Primary     | #5B5CE6 |
| Danger      | #D92D20 |

---

## 5. Title Screen

| 項目           | 仕様                       |
| ------------ | ------------------------ |
| Header Left  | Logo                     |
| Header Right | Login / 新規作成             |
| Main Left    | App Name / はじめる          |
| Main Right   | CSSアニメーション               |
| CTA          | はじめる → `/canvas`         |
| Login        | Login Modal表示            |
| Signup       | CreateNewAccount Modal表示 |

### Title Animation

```txt
Line → Mirror → Rotate & Duplicate → Pattern
```

| 項目           |         値 |
| -------------- | --------: |
| Header Height  |      56px |
| Hero Padding   |      64px |
| CTA Height     |      48px |
| Animation Area | 513 x 513 |

---

## 6. Main Screen

| 領域             | 仕様                                              |
| --------------- | ------------------------------------------------- |
| Header          | Logo / Mode Tabs / Save / Download / User         |
| Left Toolbar    | Pen / Eraser / Color / Size / Contrast / Undo / Redo |
| Canvas Area     | 描画領域                                           |
| Right Inspector | 歯車押下時のみ表示                                   |

| 項目                    |           基準値 | 採用値 |
| --------------------- | ------------: | --: |
| Left Toolbar Width    |          72px |     |
| Canvas Stage          |   856 x 744px |     |
| Drawing Canvas        |   744 x 744px |     |
| Logical Canvas        | 1024 x 1024px |     |
| Mode Tabs Width       |         480px |     |
| Mode Tab Height       |          48px |     |
| Right Inspector Width |     320〜336px |     |

---

## 7. Right Inspector

| 項目              | 仕様                     |
| ---------------- | ------------------------ |
| 初期状態          | 非表示                    |
| 表示条件          | 歯車押下                  |
| 表示形式          | 右側Overlay              |
| 閉じる操作        | Close / ESC / 外側クリック |
| Canvas再レイアウト | しない                   |

### Section

1. Mode Params
2. Light / Shadow
3. Brush Details
4. Advanced

| 項目           |         値 |
| ------------- | ---------: |
| Width         | 320〜336px |
| Padding       |       16px |
| Header Height |       48px |
| Section Gap   |       16px |

---

## 8. Auth Modal

| Modal            | 入力項目                        | 主操作         |
| ---------------- | ------------------------------ | ------------- |
| Login            | email / password               | ログインする    |
| CreateNewAccount | email / password / password確認 | 登録する       |
| ResetPassword    | email                          | 再設定メール送信 |

| 項目            |       値 |
| ------------- | --------: |
| Width         |     560px |
| Padding       |      32px |
| Input Width   | 376〜400px |
| Input Height  |      48px |
| Button Width  | 280〜320px |
| Button Height |      48px |
| Close Button  | 48 x 48px |

### 表示ルール

| URL / 操作  | 表示                           |
| ---------- | ------------------------------ |
| `/login`   | Title + Login Modal            |
| `/signup`  | Title + CreateNewAccount Modal |
| `/reset`   | Title + ResetPassword Modal    |
| Guest Save | Main Screen + Login Modal      |

---

## 9. UserName Modal

| 項目          | 仕様                   |
| ------------ | ---------------------- |
| 入力          | ユーザー名               |
| 主操作        | 登録する                 |
| 表示タイミング | 新規登録後 / MyPage変更時 |

| 項目            |   基準値 |
| ------------- | ----: |
| Width         | 560px |
| Input Height  |  48px |
| Button Height |  48px |

---

## 10. 状態設計

| 対象       | 必要状態                              |
| --------- | ------------------------------------ |
| Input     | Normal / Focus / Error / Disabled    |
| Button    | Default / Hover / Disabled / Loading |
| Modal     | Open / Close                         |
| Inspector | Closed / Open                        |
| Save      | Guest / Logged-in / Saving / Error   |

---

## 11. エラー表示位置

| エラー          | 表示位置             |
| -------------- | ------------------ |
| 未入力          | 対象Input下         |
| メール形式不正   | email Input下       |
| パスワード不一致 | password確認Input下  |
| 認証失敗        | Button上部          |
| 通信失敗        | Button上部          |
| 保存失敗        | Toast または Modal内 |

---

## 12. 実装固定ルール

* Canvasを主役にする
* Auth UIはModalで表示する
* `/login` `/signup` `/reset` のルートは残す
* Right Inspectorは初期非表示
* Modalを閉じてもCanvas状態を破棄しない
* Title右側はCSSアニメーションで表現する
* Button / Input は48px以上を基準にする

