---
title: 保護されている出力の構成
description: 保護されている出力の構成
ms.assetid: ff740b37-6e4a-4243-8e83-97dc2a46e3f1
keywords:
- OPM WDK の表示、保護されている出力の構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5256ac7da2398f628bbc63530114b1fb8793183d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375393"
---
# <a name="configuring-a-protected-output"></a>保護されている出力の構成


ディスプレイのミニポート ドライバーでは、グラフィックス アダプターの物理出力コネクタに関連付けられている保護された出力を構成する要求を受信できます。 ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数へのポインターを渡される、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)保護された出力を構成する方法を指定する構造体。 **GuidSetting**と**abParameters** DXGKMDT のメンバー\_OPM\_構成\_パラメーターは、構成の要求を指定します。

**注**  する前に**DxgkDdiOPMConfigureProtectedOutput**返します、ディスプレイのミニポート ドライバーは、ことを確認する必要があります、1 つのキー暗号化ブロック チェーン (CBC) のあるモード メッセージ認証コード (OMAC)指定されている、 **omac** DXGKMDT のメンバー\_OPM\_構成\_パラメーターが正しい。 OMAC を確認する方法の詳細については、次を参照してください。 [OMAC 1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)します。 ドライバーを確認する必要がありますも、シーケンス番号で指定された、 **ulSequenceNumber** DXGKMDT のメンバー\_OPM\_構成\_パラメーターが、シーケンスと一致するドライバーの数値現在が格納されます。 ドライバーでは、ストアドのシーケンス番号を増やす必要がありますから。

 

ディスプレイのミニポート ドライバーでは、次の構成要求をサポートする必要があります。

-   [保護されている出力の保護レベルの設定](setting-the-protection-level-for-a-protected-output.md)

-   [ビデオ信号の保護を構成します。](configuring-protection-for-the-video-signal.md)

-   [HDCP SRM バージョンを設定します。](setting-the-hdcp-srm-version.md)

 

 





