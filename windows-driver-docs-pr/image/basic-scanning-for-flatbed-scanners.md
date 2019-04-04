---
title: フラットベッド スキャナー用基本スキャン
description: フラットベッド スキャナー用基本スキャン
ms.assetid: a1100a8d-752a-4109-b1dc-cf7c4bf5a100
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d06ef7b2635bb80ec3aaed528052ebd94527f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580196"
---
# <a name="basic-scanning-for-flatbed-scanners"></a>フラットベッド スキャナー用基本スキャン





WIA アプリケーションでは、ルート項目とスキャナーのサポートされる機能を決定するスキャナー項目ツリーの最上位レベルの子項目を列挙します。 その後、アプリケーションは、スキャンのソースとしてこの子項目を使用します。 たとえば、フラット ベッド スキャナーの項目は項目がフィーダーが使用されるドキュメント フィーダーのスキャン中に、ベッドからスキャンは使用され、具合です。

Windows Vista でのフラット ベッド項目のプログラミングとスキャン動作し、Windows XP および Windows me で使用されているオーバー ロードのシステムと同じです。 このオーバー ロードのシステムは、すべて WIA 属性フラグの上に配置することで、項目のツリーの最初の子項目をプログラムします。

スキャナーのフラット ベッドをプログラムとは必ずしもこの順序で、アプリケーションは通常、次の操作に従います。

-   WIA の最上位の項目を列挙しでマークされている項目を参照、 **WiaItemTypeProgrammableDataSource**項目のフラグを使用して、 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581) WIA に設定するプロパティ\_カテゴリ\_ベッドします。

-   有効な値を読み取り、 [ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)と[ **WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)プロパティ。

-   いずれか、メモリ転送またはファイル転送の種類を選択、WIA を設定して\_IPA\_TYMED プロパティ。 転送の使用可能な種類の詳細については、[Data Transfers](data-transfers.md)を参照してください。 **IStream**-ベースの転送では、WIA\_IPA\_TYMED に既定では、フラグを設定してください。\_ファイルと、変更しないでください。

-   データの最終的な形式を選択して、WIA を設定して\_IPA\_FORMAT プロパティ。

-   イメージの設定を選択します[ **WIA\_IPA\_深さ**](https://msdn.microsoft.com/library/windows/hardware/ff551546)と[ **WIA\_IPA\_DATATYPE**](https://msdn.microsoft.com/library/windows/hardware/ff551543)。

-   この WIA 項目を使用してデータを転送します。

スキャンするスキャナーのフラット ベッドを使用する場合、ドライバーは通常、次の操作に従います。

1.  呼び出す[ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)と[ **IWiaMiniDrv::drvReadItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545005)します。 WIA ドライバーでは、アプリケーションのプロパティ設定フェーズ中にプロパティの設定を検証する必要があります。

2.  呼び出す[ **IWiaMiniDrv::drvWriteItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545020)します。 渡される WIA コンテキスト アイテムは、ドライバーは、アプリケーションがスキャナーのフラット ベッドを使用してスキャンすることを認識できるように、フラット ベッド スキャナーの項目に属しています。

3.  呼び出す[ **IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956)します。 渡される WIA コンテキスト アイテムは、ドライバーは、アプリケーションがフラット ベッドからプラテン上を使用してスキャンを予定して簡単に判断できるように、フラット ベッド スキャナーのアイテムに属しています。

4.  デバイスをプログラミングし、現在のフラット ベッド項目プロパティを使用して、フラット ベッドからスキャンします。 フラット ベッド スキャン モードで、WIA ドライバーがない場合は、スキャンは、このモードに切り替えるに試みる必要があります。 フラット ベッドを使用するアプリケーションを切り替えるの特別な設定はありません。 アプリケーションとドライバーの間のコントラクトは、フラット ベッドの項目を使用してスキャンするにはデータ転送に使用する、フラット ベッドが同意します。

ドライバーする必要があります、WIA プロパティを使用してフラット ベッド スキャナーの項目を設定として、スキャンの前に、スキャナーのフラット ベッドの一部に適用します。 WIA ドライバーによって返されるデータのヘッダーを常に信頼するには、WIA アプリケーションが必要です。 たとえば、スキャナーおよび判断された場合、指定した幅の画像をスキャンすることはできません、その結果でスキャンできる幅の値を丸めます、ドライバーがイメージ ヘッダーを幅が変更された情報に更新する必要があります。 この更新プログラムにより、正しい情報が、アプリケーションに対して使用できます。 WIA ドライバーが必要があります、デバイスから返される実際の情報に WIA プロパティを更新しようとしています。

### <a name="advanced-scanning-for-flatbed-scanners"></a>詳細なフラット ベッド スキャナーのスキャン

マルチリー ジョンのスキャン、ベッドからはどちらも手動で構成または自動的を使用して、 [WIA セグメンテーション フィルター](wia-segmentation-filter.md)。 セグメント化フィルターができること確認と、実行できないことで、アプリケーションから同じことに注意してください。 スキャンの新しいリージョンの子項目を作成するアプリケーションによって直接、セグメント化フィルターの説明されているのと同じ手順を実行できます。

 

 




