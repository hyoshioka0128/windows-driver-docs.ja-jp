---
title: HDCP SRM バージョンの設定
description: HDCP SRM バージョンの設定
ms.assetid: 23f99f8f-7d13-4868-84fb-49245a81958b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193c8db216f7a02a907c4e1b91971e39d926b942
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577909"
---
# <a name="setting-the-hdcp-srm-version"></a>HDCP SRM バージョンの設定


OPM 構成では、バージョンの高帯域幅デジタル コンテンツの保護 (HDCP) システム Renewability メッセージ (SRM) の保護された出力を設定できます。 バージョンを設定する、ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)関数へのポインターを受け取る、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560849)構造体、 **guidSetting**メンバー設定、DXGKMDT\_OPM\_設定\_HDCP\_SRM GUID と**abParameters**メンバーへのポインターに設定する[ **DXGKMDT\_OPM\_設定\_HDCP\_SRM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560915)構造体。 DXGKMDT\_OPM\_設定\_HDCP\_SRM\_パラメーター構造体には、バージョン番号を指定する ULONG が含まれています。 最下位ビット (ビット 0 ~ 15) には、リトル エンディアン形式で SRM のバージョン番号が含まれます。 SRM バージョン番号の詳細については、次を参照してください。、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)します。

 

 





