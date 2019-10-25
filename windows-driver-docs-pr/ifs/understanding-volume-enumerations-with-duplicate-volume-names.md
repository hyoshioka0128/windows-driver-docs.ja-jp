---
title: ボリューム名が重複するボリュームの列挙について
description: ボリューム名が重複するボリュームの列挙について
ms.assetid: c05982dc-4124-4f9a-93b8-0e56ac296d1b
keywords:
- ボリューム WDK ファイルシステム、重複する名前
- ボリューム WDK ファイルシステム、列挙
- フィルターマネージャー WDK ファイルシステムミニフィルター、ボリューム
- 重複するボリューム名 WDK ファイルシステム
- ボリュームの列挙 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3def983b51fb587531dec2b0d0fb20c2a89f6a1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840946"
---
# <a name="understanding-volume-enumerations-with-duplicate-volume-names"></a>ボリューム名が重複するボリュームの列挙について


ボリュームを列挙するときに、結果のボリューム情報の一覧に重複するボリューム名が表示される可能性があります。

これが発生する理由を理解するために、次のシナリオを考えてみます。ボリューム列挙ルーチン[**FltEnumerateVolumeInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumeinformation)は、すべてのシステムボリュームを列挙するために使用されます。 これにより、フィルターマネージャーが認識しているボリュームごとに1つずつ、ボリューム情報構造を格納したバッファーが生成されます。 このバッファーでは、各ボリューム情報構造は、[**フィルター\_ボリューム\_基本的な\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_basic_information)または[**フィルター\_ボリューム\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_standard_information)ですが、両方を指定することはできません。

このボリューム情報構造の一覧を指定すると、複数のリスト要素に同じボリューム名を含めることができます。 つまり、2つ以上のリスト要素の**filtervolumename**メンバーが同一である可能性があります。 これが可能なのは、 [**FltEnumerateVolumes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumes)などのすべてのフィルターマネージャー列挙ルーチンが、マウント解除されていても破棄されていないボリューム (開いているファイルがまだボリューム上に存在しているため) を含むボリュームを列挙するためです。 このため、ボリュームのマウントが解除されると、ボリューム情報リスト (現在のマウントされた状態の場合は1回、前のマウント解除された状態の場合は1回、最も単純な場合は非破棄状態) で、ボリュームの名前が複数回表示されることがあります。

ボリューム情報の一覧に重複するボリューム名が表示される場合は、同じ名前の各グループが前述の説明によって説明されています。 ただし、上記のシナリオを確認するには、次の手順を実行します。

-   フィルター\_ボリューム\_標準\_情報の構造を使用してリストに値が設定されている場合は、 **filtervolumename**メンバーが等しい構造体のグループを識別します。 このグループ内の1つまたは複数の構造体が、**フラグ**メンバーで設定されている\_ボリュームフラグを\_\_している場合は、そのグループに関連付けられているボリュームがマウント解除されていますが、非破棄状態になっています。 これにより、重複するボリューム名が存在することが確認できます。 該当する場合は、残りのすべてのグループに対してこの手順を繰り返します。

-   リストに type of FILTER\_VOLUME\_BASIC\_INFORMATION の構造が設定されている場合は、この一覧を同等のフィルター\_ボリューム\_標準\_情報構造体の形式に変換して、前の例のように処理します。ブレットポイント。

フィルター\_ボリューム\_標準\_情報の構造は、Windows Vista 以降でのみ使用でき  **ことに注意**してください。

 

このトピックの影響を受けるルーチンと構造は次のとおりです。

[ **\_ボリューム\_基本的な\_情報にフィルターを適用する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_basic_information)

[ **\_ボリューム\_標準\_情報をフィルター処理する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_standard_information)

[**FilterVolumeFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindfirst)

[**FilterVolumeFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindnext)

[**FltEnumerateVolumeInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumeinformation)

[**FltEnumerateVolumes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumes)

[**FltGetVolumeInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumeinformation)

 

 




