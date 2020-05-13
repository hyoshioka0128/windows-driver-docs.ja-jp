---
title: Windows ハードウェアエラーアーキテクチャ (WHEA) の概要
description: Windows ハードウェアエラーアーキテクチャ (WHEA) の概要
ms.assetid: 5a0bbf8c-d644-4a64-9a7e-400d5de2c8fa
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、Windows ハードウェアエラーアーキテクチャについて
- WHEA WDK、Windows ハードウェアエラーのアーキテクチャについて
- ハードウェアエラー WDK WHEA、Windows ハードウェアエラーアーキテクチャについて
- エラー WDK WHEA、Windows ハードウェアエラーアーキテクチャについて
- ソース情報 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91981868b76739cd9ca9eacf66c0cdb628c75521
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235443"
---
# <a name="introduction-to-the-windows-hardware-error-architecture"></a>Windows Hardware Error Architecture の基本

Windows Vista で導入された Windows ハードウェアエラーアーキテクチャ (WHEA) は、以前のハードウェアエラー報告メカニズムを拡張し、一貫したハードウェアエラーインフラストラクチャのコンポーネントとしてまとめています。 WHEA は、現在のハードウェアデバイスで利用可能な追加のハードウェアエラー情報を利用し、システムファームウェアにより密接に統合します。

その結果、WHEA には次のような利点があります。

-   では、ハードウェアエラーの根本原因を特定するために、標準のエラーレコード形式でより広範なエラーデータを使用できるようになりました。

-   ハードウェアエラーからの回復を支援するメカニズムを提供します。ハードウェアエラーが致命的でない場合に、バグチェックが発生しないようにします。

-   は、ユーザーモードエラー管理アプリケーションをサポートし、Windows イベントトレーシング (ETW) イベントを使用した高度なシステム正常性監視と、エラー管理と制御のための API を提供します。

-   には拡張性があり、ハードウェアベンダーがデバイスに新しいハードウェアエラー報告メカニズムを追加すると、WHEA により、オペレーティングシステムは新しいメカニズムに対応できるようになります。

