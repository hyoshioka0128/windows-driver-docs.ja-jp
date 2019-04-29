---
title: トラステッド プラットフォーム モジュール (TPM) に関する考慮事項
description: トラステッド プラットフォーム モジュール (TPM) に関する考慮事項
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e8ba6645ef8d5feef02e363898ea030822847814
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337385"
---
# <a name="trusted-platform-module-tpm-considerations"></a>トラステッド プラットフォーム モジュール (TPM) に関する考慮事項

TPM 2.0 によって、新しいデバイスは、すべての PCR バンクに SHA256 を使用します。 これはダウンレベル オペレーティング システムと互換性がない可能性があります。

TPM 2.0 に従来の BIOS インターフェイスはありません。 ただし、これらのシナリオでは、Bitlocker で TPM 2.0 を利用できます。  を現在のハードウェアに Windows 7 をインストールする必要がありますでインストール x64 UEFI ブート モード (ただし、Windows 7 のブートの要件により、CSM が必要になります) TPM 2.0 からいくつかの利点を受信できるようにされます。

以降のオペレーティング システムにアップグレードした後 (Win8 以降)、によって、システムにインストールされているファームウェア、セキュア ブートを有効にする機能があります。 既存のハードウェア上の従来の BIOS モードで Windows オペレーティング システムをインストールする場合は、TPM 2.0 またはセキュア ブートのすべてのメリットを受信できません。

## <a name="related-resources"></a>関連リソース

[TPM の推奨事項](https://docs.microsoft.com/windows/security/hardware-protection/tpm/tpm-recommendations)

[トラステッド プラットフォーム モジュール 2.0:簡単な概要について](http://www.trustedcomputinggroup.org/trusted-platform-module-2-0-brief-introduction/)

[トラステッド プラットフォーム モジュール (TPM)](http://www.trustedcomputinggroup.org/work-groups/trusted-platform-module/)




