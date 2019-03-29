---
title: Sdv-map.h
description: Sdv-map.h
ms.assetid: c230fb86-fe65-416b-bd3e-a0ab7270576d
keywords:
- 出力ファイルは、WDK Static Driver Verifier
- Sdv map.h WDK Static Driver Verifier
- ヘッダー ファイルの WDK Static Driver Verifier
- WDK Static Driver Verifier のドライバー エントリ ポイントします。
- WDK Static Driver Verifier のエントリ ポイントします。
- Sdv map.h についての Sdv map.h WDK Static Driver Verifier
- DriverEntry ルーチン WDK Static Driver Verifier のスキャン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02ee90b793f42a3150612dfc97be2ed6ade6d323
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581863"
---
# <a name="sdv-maph"></a>Sdv-map.h


Sdv map.h は、SDV は、ドライバーで検出されたドライバーのエントリ ポイントを一覧表示するヘッダー ファイルです。

SDV は、使用すると、ドライバーのソース ディレクトリに Sdv map.h ファイルを作成、 **staticdv/scan**ドライバーのソース コードをスキャンするコマンド。 SDV は、関数の役割の型宣言を使用して、エントリ ポイントを特定します。 使用しない場合、 **staticdv/scan**コマンドを使用すると、SDV は Sdv map.h ファイルを作成、 **staticdv/check** SDV 分析を実行するコマンド。

このファイルが不正確または不完全な場合、修正、承認、および再スキャンし、検証を再実行します。

このセクションの内容:

[Understanding の Sdv map.h](understanding-the-sdv-map-h-file.md)

[Sdv map.h 形式](format-of-the-sdv-map-h-file.md)

[Sdv map.h を承認します。](approving-the-sdv-map-h-file.md)

[関数のロールの種類のエントリ ポイントを重複しています](duplicate-entry-points-for-a-function-role-type.md)

 

 





