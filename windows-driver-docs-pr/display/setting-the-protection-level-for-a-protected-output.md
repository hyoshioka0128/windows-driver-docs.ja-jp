---
title: 保護されている出力の保護レベルの設定
description: 保護されている出力の保護レベルの設定
ms.assetid: 2f041190-8001-4e79-8398-8b642884f751
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1423974d09b271acc21b8d2781aa814bb2e5fbaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350213"
---
# <a name="setting-the-protection-level-for-a-protected-output"></a>保護されている出力の保護レベルの設定


OPM 構成では、保護された出力を保護の種類の保護レベルを設定できます。 レベルを設定する、保護、ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)関数へのポインターを受け取る、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560849)構造体、 **guidSetting**メンバー設定、DXGKMDT\_OPM\_セット\_保護\_レベル GUID と**abParameters**メンバーへのポインターに設定する[ **DXGKMDT\_OPM\_設定\_保護\_レベル\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560921)セットと、保護を設定するレベルに保護の種類を指定する構造体。 指定した保護の種類は、次の保護レベルを設定できます。

-   DXGKMDT の\_OPM\_保護\_型\_ACP がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_から保護レベル値のいずれかのパラメーター、 [ **DXGKMDT\_OPM\_ACP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560834)で列挙型を指定することができます、 **ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

-   DXGKMDT の\_OPM\_保護\_型\_CGMSA がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_から保護レベル値のいずれかのパラメーター、 [ **DXGKMDT\_OPM\_CGMSA** ](https://msdn.microsoft.com/library/windows/hardware/ff560846)列挙型指定することができます、 **ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

-   DXGKMDT の\_OPM\_保護\_型\_HDCP または DXGKMDT\_OPM\_保護\_型\_COPP\_互換性のある\_HDCP がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_のいずれかのパラメーター、保護レベルの値から、 [ **DXGKMDT\_OPM\_HDCP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560878)で列挙型を指定することができます、**ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

-   DXGKMDT の\_OPM\_保護\_型\_DPCP がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_から保護レベル値のいずれかのパラメーター、 [ **DXGKMDT\_OPM\_DPCP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560861)で列挙型を指定することができます、 **ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

**注**   、DXGKMDT\_OPM\_設定\_保護\_レベル\_ACCORDING\_TO\_CSS\_DVD の GUID はの新機能Windows 7 をドライバーに新しい CSS 規則に従った HDCP が有効にすることを示すために使用されます。 設定、DXGKMDT\_OPM\_設定\_保護\_レベル\_ACCORDING\_TO\_CSS\_DVD コマンドは既存の DXGKMDT の設定と同じ\_OPM\_設定\_保護\_レベルのコマンドを除くその DXGKMDT\_OPM\_設定\_保護\_レベル\_に従って\_TO\_CSS\_DVD に要求された保護を有効にする絶対要件がありません。

 

 

 





