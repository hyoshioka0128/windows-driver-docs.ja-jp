---
title: ミニドライバーの INI ファイルの BidiFiles エントリ
description: ミニドライバーの INI ファイルの BidiFiles エントリ
ms.assetid: 953a29d2-f778-410e-bc8a-a09e294f2473
keywords:
- BidiFiles セクション
- WDK の INF ファイルの印刷、双方向の拡張機能ファイルの情報
- 双方向の拡張機能は、WDK プリンター autoconfig をファイルします。
- ボックスの自動構成サポートの WDK プリンター、双方向の拡張ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3eacbaaada4df272c7b6e079d2acb2afe3e4b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550038"
---
# <a name="bidifiles-entry-in-a-minidrivers-ini-file"></a>ミニドライバーの INI ファイルの BidiFiles エントリ


プリンター ミニドライバーは、ミニドライバーに固有の INI ファイルを使用して、ポート モニターを双方向の拡張ファイルに関する情報を通信します。 ポート モニターには、ポートの初期化中には、この情報が使用されます。

次のサンプルに示します、 `BidiFiles` INI ファイルのセクション。 `BidiSPMFile`エントリに使用される標準の TCP/IP ポート モニタと`BidiWSDFile`エントリ Devices (WSD) ポート モニター用の Web サービスに使用されます。

```INI
# OEM Mapping & Extension GDL files 
# 
[BidiFiles]
BidiSPMFile = BidiSPM_AcmeXXX.XML
BidiWSDFile  = BidiWSD_AcmeXXX.XML
```
