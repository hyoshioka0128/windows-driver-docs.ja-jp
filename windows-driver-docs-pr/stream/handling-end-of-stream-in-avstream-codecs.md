---
title: AVStream コーデックで Stream の最後の処理
description: AVStream コーデックで Stream の最後の処理
ms.assetid: ee57137b-999a-449f-9f9d-50bc19e07ba8
keywords:
- WDK AVStream のストリームの末尾の処理
- WDK AVStream のストリームの末尾
- ハードウェアのコーデック サポート WDK AVStream、ストリームの末尾
- AVStream ハードウェア コーデックは、WDK、ストリームの末尾の処理をサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eeff1d7677e08e40fb00f431ea9df7b9a061d36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528428"
---
# <a name="handling-end-of-stream-in-avstream-codecs"></a>AVStream コーデックで Stream の最後の処理


KSSTREAM HW MFT は、ストリーム (EOS) フラグのセットの末尾を使用するサンプルを受信すると、設定\_ヘッダー\_OPTIONSF\_で ENDOFSTREAM、 **OptionsFlag**のメンバー、 [ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)サンプルに対応する構造体。

ミニドライバーを受信した後、 [ **KSSTREAM\_ポインター** ](https://msdn.microsoft.com/library/windows/hardware/ff567139) 、KSSTREAM で\_ヘッダー\_OPTIONSF\_に設定されるENDOFSTREAMフラグ**StreamHeader.OptionsFlag**、ミニドライバー KSSTREAM に設定されるまでは、入力ピンは、新しい入力ストリーム ポインターを受け取りません\_ヘッダー\_OPTIONSF\_出力ストリームに ENDOFSTREAM。ポインター。

ミニドライバー KSSTREAM を設定する前に\_ヘッダー\_OPTIONSF\_現在使用できる入力で実現可能な数の出力のフレームが生成する出力ストリーム ポインターを ENDOFSTREAM、します。

ミニドライバーは、これらのストリーム ポインターに関連付けられているデータだけでなく、以前に処理されたストリーム ポインターに関連する情報をキャッシュいずれかのチェック ボックスをオフにし、必要があります。 ミニドライバーは KSSTREAM を設定する必要があります\_ヘッダー\_OPTIONSF\_出力ピン ENDOFSTREAM します。

ミニドライバーは、新しいストリームの一部として、その後に到着した新しい入力ストリーム ポインターを扱う必要があります。 メディア ストリームを連続していない結果として、EOS が発生したかどうかは例外です。 大文字と小文字の場合は、新しく到着するストリーム ポインターが、KSSTREAM\_ヘッダー\_OPTIONSF\_DATADISCONTINUITY または KSSTREAM\_ヘッダー\_OPTIONSF\_TIMEDISCONTINUITY、またはKSSTREAM で設定されているフラグの両方、\_ヘッダー **。OptionsFlags**します。 これらのフラグを設定のいずれかを含むストリーム ポインターは、入力ピンに到着、ミニドライバーは、対応する出力ピンのストリーム ポインターを同じフラグを設定する必要があります。

 

 




