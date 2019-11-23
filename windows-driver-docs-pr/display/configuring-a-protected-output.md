---
title: 保護されている出力の構成
description: 保護されている出力の構成
ms.assetid: ff740b37-6e4a-4243-8e83-97dc2a46e3f1
keywords:
- OPM WDK 表示、保護された出力の構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0de7f1fa5a6a7ec1eca3a062141900af5cae25d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839795"
---
# <a name="configuring-a-protected-output"></a>保護されている出力の構成


ディスプレイミニポートドライバーは、グラフィックスアダプターの物理出力コネクタに関連付けられている保護された出力を構成する要求を受信できます。 表示ミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数には、 [**Dxgkmdt\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)へのポインターが渡され、保護された出力の構成方法を指定する\_PARAMETERS 構造\_構成します。 DXGKMDT\_OPM の**Guidsetting**および**abparameters**メンバーは、構成要求を指定し\_パラメーターを構成\_ます。

**DxgkDdiOPMConfigureProtectedOutput**が返される前に、表示ミニポートドライバーは、DXGKMDT の**omac**メンバーに指定されている1つの暗号ブロックチェーン (CBC) モードのメッセージ認証コード (omac) が、\_のパラメーターを構成\_\_、**正しいことを**確認する必要があります。   OMAC の検証の詳細については、「 [omac-1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)」を参照してください。 また、ドライバーは、DXGKMDT\_\_\_OPM の**ulSequenceNumber**メンバーに指定されているシーケンス番号が、ドライバーに現在格納されているシーケンス番号と一致することを確認する必要があります。 次に、ドライバーは、格納されているシーケンス番号をインクリメントする必要があります。

 

ディスプレイミニポートドライバーは、次の構成要求をサポートしている必要があります。

-   [保護された出力の保護レベルの設定](setting-the-protection-level-for-a-protected-output.md)

-   [ビデオ信号の保護の構成](configuring-protection-for-the-video-signal.md)

-   [HDCP の SRM バージョンの設定](setting-the-hdcp-srm-version.md)

 

 





