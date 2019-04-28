---
title: ファイル システムのセキュリティの概要
description: ファイル システムのセキュリティの概要
ms.assetid: 328568dc-a003-4e00-941a-9ccf15b1c735
keywords:
- セキュリティ WDK ファイル システム、ファイル システムのセキュリティについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac35e0c8f147768c762ee5e9d635009bb54f2392
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379722"
---
# <a name="introduction-to-file-systems-security"></a>ファイル システムのセキュリティの概要


## <span id="ddk_introduction_to_file_systems_security_if"></span><span id="DDK_INTRODUCTION_TO_FILE_SYSTEMS_SECURITY_IF"></span>


WDK を使用するファイル システムの開発者は、ファイル システムの実装時にセキュリティの考慮事項に注意してくださいあります。 ファイル システム フィルター ドライバー開発者は、これらの問題では、注意すべきし、セキュリティに関する考慮事項を自社製品に組み込むためには使い慣れた Microsoft Windows セキュリティ インターフェイスを使用する必要があります。

このセクションでは、Windows のセキュリティとファイル システムに重点を置いています。 Windows、またはファイル システムの開発者に Windows 環境で Windows 以外のセキュリティ モデルを実装する場合は、セキュリティ拡張機能を開発する必要がある場合、入門書にするものではありません。

このセクションには、多くサンプル コードにはが含まれています。 サンプルでは、実際のコードから抽出されますが、省略形でここに表示されます。 開発者は、特定の環境で使用するため、これらのサンプルを調整する必要があります。

 

 




