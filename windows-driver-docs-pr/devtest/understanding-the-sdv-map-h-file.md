---
title: Sdv map.h ファイルを理解します。
description: Sdv map.h ファイルを理解します。
ms.assetid: 2ad3d94d-3991-414b-ae1c-27a07c10839f
keywords:
- Sdv map.h についての Sdv map.h WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0db80cf0bfa5d1389258c4760999607dd5b54242
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529412"
---
# <a name="understanding-the-sdv-maph-file"></a>Sdv map.h ファイルを理解します。


ドライバーを検証する前に、SDV は、ドライバーのソース コードをスキャンし、ドライバーのソース ディレクトリに Sdv map.h ファイルを作成します。 調べるには、ドライバーを検証する前にこのヘッダー ファイルを承認してください。

使用することも、 **staticdv/scan**ドライバーをスキャンする SDV を指示するコマンドのコードし、ファイルを作成します。 手順については、次を参照してください。[ドライバーをスキャン](scanning-the-driver.md)します。

Sdv map.h ファイルが不完全なまたは正しくない場合は、エントリ ポイントのいずれかが存在しないか、またはエントリ ポイントは、間違った関数ロールの種類に関連付けられている場合、検証は信頼できません。

WDM、KMDF、NDIS ドライバーに SDV を使用する関数の一覧は、次を参照してください。[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。

Sdv map.h ファイルに表示される関数のロールの種類は、SDV は、そのルールの検証で使用するものです。 SDV は、ドライバーのソース コード ディレクトリに Sdv map.h ファイルを生成するために、ヘッダー ファイルに追加した関数の役割型の宣言を使用します。 Sdv map.h ファイルでは、SDV は、SDV での検証中に使用される関数識別子にドライバーが宣言された関数をマップします。 たとえば、KMDF ドライバーでは、コールバック関数という*MyDpc*マップすることがあります楽しいに\_WDF\_DPC\_1。 

SDV では、ドライバーが使用するコールバック関数のすべてのロールの種類について関数を宣言している必要はありません。 するだけです、ドライバーには、関数のロールの種類が宣言されている場合その SDV 認識で正しく解釈されます。 ドライバーでは、SDV は、特定のルールを確認する必要があります関数ロールの種類はありません、SDV は、ルールは、ドライバーには適用されませんを終了します。 これはエラーや障害にすると見なされません。 

ドライバーを検証する前に、Sdv map.h ファイル内のエラーを修正することが重要です。 ファイルが間違っている場合、検証を信頼できない可能性があります。

 

 





