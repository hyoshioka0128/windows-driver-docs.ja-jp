---
title: 重複するボリューム名がある場合のボリュームの列挙について
description: 重複するボリューム名がある場合のボリュームの列挙について
ms.assetid: c05982dc-4124-4f9a-93b8-0e56ac296d1b
keywords:
- WDK のボリュームのファイル システム、重複する名前
- WDK のボリュームのファイル システムを列挙します。
- フィルター マネージャー WDK ファイル システム ミニフィルター、ボリューム
- 重複するボリューム名 WDK ファイル システム
- WDK ファイル システムのボリュームを列挙します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a60af89126e6cce160d1149a6b168f0ffaea8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350032"
---
# <a name="understanding-volume-enumerations-with-duplicate-volume-names"></a>重複するボリューム名がある場合のボリュームの列挙について


ボリュームを列挙するときに、重複するボリューム名結果として得られるボリューム情報の一覧に表示される可能性があります。

これが発生する理由を理解するために、次のシナリオを検討してください。 ボリューム列挙ルーチン[ **FltEnumerateVolumeInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff542091)すべてのシステム ボリュームを列挙するために使用します。 これにより、フィルター マネージャーに既知のボリュームごとに 1 つのボリューム情報の構造に格納するバッファー。 このバッファーには各ボリューム情報の構造体の型指定できます[**フィルター\_ボリューム\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff541631)または[ **フィルター\_ボリューム\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff541647)、両方ではないです。

ボリューム情報の構造体のこのリストを指定するには、可能性が同じボリュームの名前を格納する複数のリストの要素です。 つまり、 **FilterVolumeName**リストの要素が 2 つ以上のメンバーは、同一である可能性があります。 これは、すべてのフィルター マネージャー列挙ルーチンでは、ため可能[ **FltEnumerateVolumes**](https://msdn.microsoft.com/library/windows/hardware/ff542092)ボリュームがマウント解除されていますが、破損ダウンされていないものも含めての列挙 (ために、ファイルを開くこともボリューム上に存在します)。 そのため、ボリュームがマウント解除、ボリューム情報の一覧 - でその名前を複数回出現できるとき 1 回、マウントされた現在の状態とその前に 1 回のマウント解除されますが、最も簡単なケースでの非破損ダウン状態。

重複するボリューム名は、ボリューム情報の一覧に表示する場合と同じ名前の各グループは、上記の説明で説明します。 ただしは、次の手順を使用して、上記のシナリオを確認できます。

-   一覧のフィルターの型の構造体は、\_ボリューム\_標準\_については、構造のグループを識別が**FilterVolumeName**メンバーが等しい。 このグループ内の構造体の 1 つ以上が、FLTFL\_VSI\_DETACHED\_ボリューム フラグを設定、**フラグ**で、マウント解除されたが破損ダウン以外で、メンバー グループに関連付けられているボリュームは状態。 これは、重複するボリューム名が存在する理由を確認します。 該当する場合は、このようなすべての残りグループに対してこの手順を繰り返します。

-   一覧のフィルターの型の構造体は、\_ボリューム\_BASIC\_については、この一覧にその同等のフィルター変換\_ボリューム\_標準\_情報フォームの構造体、前の箇条書きのように進みます。

**注**   、フィルター\_ボリューム\_標準\_情報構造体は Windows Vista から使用できます。

 

ルーチンと構造体のこのトピックの「影響を受ける次に示します。

[**フィルター\_ボリューム\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff541631)

[**フィルター\_ボリューム\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff541647)

[**FilterVolumeFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff541525)

[**FilterVolumeFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541530)

[**FltEnumerateVolumeInformation**](https://msdn.microsoft.com/library/windows/hardware/ff542091)

[**FltEnumerateVolumes**](https://msdn.microsoft.com/library/windows/hardware/ff542092)

[**FltGetVolumeInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543238)

 

 




