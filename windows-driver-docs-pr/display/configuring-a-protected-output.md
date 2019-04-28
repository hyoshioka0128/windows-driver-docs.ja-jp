---
title: 保護されている出力の構成
description: 保護されている出力の構成
ms.assetid: ff740b37-6e4a-4243-8e83-97dc2a46e3f1
keywords:
- OPM WDK の表示、保護されている出力の構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5df5f4d3a89536c83e34ee5074a11a61f20cebf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376768"
---
# <a name="configuring-a-protected-output"></a>保護されている出力の構成


ディスプレイのミニポート ドライバーでは、グラフィックス アダプターの物理出力コネクタに関連付けられている保護された出力を構成する要求を受信できます。 ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)関数へのポインターを渡される、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560849)保護された出力を構成する方法を指定する構造体。 **GuidSetting**と**abParameters** DXGKMDT のメンバー\_OPM\_構成\_パラメーターは、構成の要求を指定します。

**注**  する前に**DxgkDdiOPMConfigureProtectedOutput**返します、ディスプレイのミニポート ドライバーは、ことを確認する必要があります、1 つのキー暗号化ブロック チェーン (CBC) のあるモード メッセージ認証コード (OMAC)指定されている、 **omac** DXGKMDT のメンバー\_OPM\_構成\_パラメーターが正しい。 OMAC を確認する方法の詳細については、次を参照してください。 [OMAC 1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)します。 ドライバーを確認する必要がありますも、シーケンス番号で指定された、 **ulSequenceNumber** DXGKMDT のメンバー\_OPM\_構成\_パラメーターが、シーケンスと一致するドライバーの数値現在が格納されます。 ドライバーでは、ストアドのシーケンス番号を増やす必要がありますから。

 

ディスプレイのミニポート ドライバーでは、次の構成要求をサポートする必要があります。

-   [保護されている出力の保護レベルの設定](setting-the-protection-level-for-a-protected-output.md)

-   [ビデオ信号の保護を構成します。](configuring-protection-for-the-video-signal.md)

-   [HDCP SRM バージョンを設定します。](setting-the-hdcp-srm-version.md)

 

 





