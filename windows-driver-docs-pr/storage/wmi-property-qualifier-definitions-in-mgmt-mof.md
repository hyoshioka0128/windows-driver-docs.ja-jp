---
title: Mgmt.mof 内の WMI プロパティ修飾子の定義
description: Mgmt.mof 内の WMI プロパティ修飾子の定義
ms.assetid: 2d8e7e83-6304-459f-b9d8-b40365834bb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 82a2ab76b3ad2623b17851a9d094c5ef3870b7dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571242"
---
# <a name="wmi-property-qualifier-definitions-in-mgmtmof"></a>Mgmt.mof 内の WMI プロパティ修飾子の定義


## <span id="ddk_wmi_property_qualifier_definitions_in_mgmt_mof_kr"></span><span id="DDK_WMI_PROPERTY_QUALIFIER_DEFINITIONS_IN_MGMT_MOF_KR"></span>


定義されている WMI 修飾子*Mgmt.mof*の iSCSI 検出ライブラリおよびその他の管理ソフトウェアは、iSCSI イニシエーターから取得した情報を報告する使用できるデータ形式のいくつかを指定します。

*Mgmt.mof*ファイルは、次の WMI プロパティ修飾子を定義します。

[ISCSI\_接続\_状態\_型\_修飾子](iscsi-connection-state-type-qualifiers.md)

[ISCSI\_接続\_プロトコル\_型\_修飾子](iscsi-connection-protocol-type-qualifiers.md)

[ISCSI\_セッション\_型\_修飾子](iscsi-session-type-qualifiers.md)

[ISCSI\_ヘッダー\_整合性\_型\_修飾子](iscsi-header-integrity-type-qualifiers.md)

[ISCSI\_データ\_整合性\_型\_修飾子](iscsi-data-integrity-type-qualifiers.md)

[ISCSI\_ポータル\_型\_修飾子](iscsi-portal-type-qualifiers.md)

[ISCSI\_イニシエーター\_ノード\_エラー\_型\_修飾子](iscsi-initiator-node-failure-type-qualifiers.md)

[ISCSI\_イニシエーター\_エラー\_型\_修飾子](iscsi-initiator-failure-type-qualifiers.md)

WMI クラス定義内のデータ フィールドに、上記の修飾子のいずれかを適用する場合は、対応する構造体のメンバーに修飾子の定義に示される整数値のいずれかを割り当てることができますを示します。

そのため、WMI プロパティ修飾子では、修飾子は、一連の整数値を表すために列挙体が似ています。 WMI ツールのスイートで列挙型の宣言を生成しませんが、 *Iscsimgt.h*で修飾子に対応する*Mgmt.mof*、シンボリック定数の定義のセットはどちらも、生成します。修飾子の値に対応します。

WMI プロパティ修飾子の概要については、次を参照してください。 [WMI プロパティ修飾子](https://msdn.microsoft.com/library/windows/hardware/ff566365)します。

 

 





