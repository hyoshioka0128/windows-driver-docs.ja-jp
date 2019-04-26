---
title: 開始の種類値の設定
description: 開始の種類値の設定
ms.assetid: dcc38a36-4755-472b-94c8-dfed892460ee
keywords:
- INF ファイル WDK 表示の開始型の値
- 型の値を WDK の表示の開始します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0ed77239757d11b5a438867b6c43d045732a87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340418"
---
# <a name="setting-the-start-type-value"></a>開始の種類値の設定


Windows 表示 Driver Model (WDDM) オペレーティング システム上で実行したディスプレイ ドライバーの場合と同様に、オペレーティング システムの初期化中ではなく、オンデマンドで Windows Vista 以降の実行を開始するのには記述されているディスプレイ ドライバーを設定する必要があります。Windows Vista する前にします。 この変更は、マニフェストとイメージ ベース インストールできなかった機能が Windows Vista より前のオペレーティング システム上に存在するためです。 値を設定する必要があります、 **StartType**サービスへのエントリ\_デマンド\_サービスではなく (3) が開始\_システム\_(1) を開始します。

次の例では、値を持つサービス インストール セクション、 **StartType**サービス エントリを設定\_デマンド\_をオンデマンドでディスプレイのミニポート ドライバーが開始されたことを示す開始。

```inf
;
; Service Installation Section
;

[R200_Service_Inst]
ServiceType    = 1        ; SERVICE_KERNEL_DRIVER
StartType      = 3        ; SERVICE_DEMAND_START
ErrorControl   = 0        ; SERVICE_ERROR_IGNORE
LoadOrderGroup = Video
ServiceBinary  = %12%\r200.sys
```

関連付けられているセクションではサービスのインストールの詳細については、 **AddService**ディレクティブを参照してください[ **INF AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)します。

 

 





