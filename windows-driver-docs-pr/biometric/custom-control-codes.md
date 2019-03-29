---
title: カスタム コントロールのコード
description: ベンダーは、カスタム コントロールのコードを定義します。
ms.assetid: 66eebb4b-ee1e-42d2-9a4b-98a79a0f7b75
keywords:
- 生体認証ドライバー WDK、制御コード
ms.date: 11/13/2017
ms.localizationpriority: medium
ms.openlocfilehash: 969f55aecbbcc2147da842b029f53e13591c4293
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571537"
---
# <a name="custom-control-codes"></a>カスタム コントロールのコード

ベンダーは、0x800 で始まるカスタム コントロールのコードを定義できます。

ベンダー固有の I/O 制御コードを定義するには、システム提供の CTL_CODE マクロを使用して、次の引数で。

```c
#define IOCTL_BIOMETRIC_Device_Function CTL_CODE(FILE_DEVICE_BIOMETRIC, Function, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

すべての入力/出力パラメーターでは、ベンダー定義します。 **状態**メンバーは、次の表の値のいずれかに設定されます。

| 状態値 | 説明 |
| --- | --- |
| S_OK、STATUS_SUCCESS | 操作が完了しました。 返されるデータのサイズが DWORD の場合は、ペイロードには、呼び出しに必要なバッファーのサイズが含まれています。 それ以外の場合、ペイロードには、完全な出力バッファーが含まれています。 |
| E_INVALIDARG | パラメーターが正しく指定されませんでした。 |

ベンダ定義の Ioctl を任意のベンダー固有の操作に使用できます。 これらの呼び出しは、デバイスの排他的制御を持つ Windows 生体認証サービスを介して送られてきます。 ベンダーが仕入先を使用する方法の例をいくつかをここでは特定の Ioctl:

- アプリケーションまたはコンポーネントとデバイスの間の独自のセキュリティで保護されたセッションを設定します。
- WinBio エンジンまたはプラグイン データベースからデバイスに一致してストレージの機能を備えたインターフェイスします。
- デバイスのベンダー固有のイベントの I/O を保留します。
- ベンダー固有のセッションを管理します。

この機能は、Windows 7 および Windows の以降のバージョンで使用できます。


