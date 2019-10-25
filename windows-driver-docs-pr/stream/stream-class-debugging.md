---
title: ストリーム クラスのデバッグ
description: ストリーム クラスのデバッグ
ms.assetid: 544b922b-58e4-4cbb-a76c-d8e13ae17e55
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、デバッグ
- streaming ミニドライバー WDK Windows 2000 カーネル、デバッグ
- ミニドライバー WDK Windows 2000 カーネルストリーミング、デバッグ
- デバッグストリームクラスミニドライバー WDK Windows 2000 カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a571acc40cf4474938965184157d0d99db25be6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837684"
---
# <a name="stream-class-debugging"></a>ストリーム クラスのデバッグ





ミニドライバーのチェックされた (デバッグ)*バージョンを使用*して、ミニドライバー内のエラーが検出されたときに、その状態に関する情報メッセージを出力し、アサートします。

次に、ストリームクラスミニドライバーをデバッグするときに使用できるその他のヒントを示します。

-   Windows Me システムで wdeb386 デバッガー (または Softice) を使用してデバッグを行う場合、デバッガーを中断して「」と入力すると、デバッグ情報が表示されます。NTKERN をクリックし、オプション D を選択します。これにより、デバッグログが表示され、エントリが時系列順に表示されます。 Windows 2000 でデバッグする場合は、デバッグ情報がデバッグ端末にリアルタイムで出力されます。

-   デバッガーの出力レベルを調整するには、 *.sys*シンボル (windows Me の場合は*sym* 、windows 2000 の場合は *.Sys* ) を読み込み、 *streamdebug*変数を "e streamdebug *xx*" で変更します。 既定値は00で、重大なエラーのみを出力します。 すべてのメッセージを出力するには、FF に設定します。

-   ミニドライバーは、前に説明した[**Streamclassdebugprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdebugprint)を呼び出すことに*よって、* 独自のメッセージを印刷できます。 前述の出力レベルは、呼び出しで選択された出力レベル以上に設定する必要があることに注意してください。

 

 




