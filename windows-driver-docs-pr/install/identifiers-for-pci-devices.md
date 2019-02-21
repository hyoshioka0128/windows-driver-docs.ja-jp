---
title: PCI デバイスの識別子
description: PCI デバイスの識別子
ms.assetid: 58d52af8-9afd-441f-9ed9-92f9e2775226
keywords:
- デバイスの識別文字列 WDK、PCI デバイス
- 識別文字列の WDK デバイス、PCI デバイス
- 識別子の WDK デバイス、PCI デバイス
- PCI デバイス識別子 WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
- 互換性のある Id WDK デバイスのインストール
ms.date: 05/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9188b95ec43959eefd11d4eb80d9ee80d9676ad5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552559"
---
# <a name="identifiers-for-pci-devices"></a>PCI デバイスの識別子

> [!IMPORTANT]
> PCI デバイスで使用される既知の Id の一覧を検索する[、PCI ID リポジトリ](https://pci-ids.ucw.cz/)します。 リスト Id を使用して、Windows に`devcon hwids *`します。

一覧を次に、[デバイス識別文字列](device-identification-strings.md)PCI バス ドライバーはハードウェア Id を使用してフォーマットします。 プラグ アンド プレイ (PnP) マネージャーでは、ハードウェア デバイスの Id のドライバーをクエリ、PCI バス ドライバーはの汎用性の放棄の昇順にハードウェア Id の一覧を返します。

```cpp
PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)

PCI\\VEN_v(4)&DEV_d(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)p(2)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)
```

各項目の意味は次のとおりです。

-   v(4) は、デバイスのベンダーの 4 文字の PCI SIG によって割り当てられた識別子を用語*デバイス*、PCI SIG の使用状況の後、特定の PCI チップを参照します。

-   d(4) とは、デバイスの 4 文字のベンダ定義識別子です。

-   s(4) とは、4 文字のベンダ定義のサブシステムの識別子です。

-   n(4) は、サブシステムの仕入先の 4 文字 PCI SIG によって割り当てられた識別子です。

-   r(2) は、2 文字のリビジョン番号です。

-   c(2) は、構成の領域から基底クラスの 2 文字コードです。

-   s(2) は、2 文字のサブクラス コードです。

-   p(2) では、プログラミング インターフェイスのコードを示します。

次は、ポータブル コンピューターのディスプレイ アダプターのハードウェア ID の例です。 このハードウェア ID の形式は、PCI\\VEN_v(4) & DEV_d(4) & SUBSYS_s(4)n(4) REV_r(2) します。

    PCI\\VEN_102C&DEV_00E0&SUBSYS_00000000&REV_04

リビジョン情報が削除では、前の例では、ディスプレイ アダプターのハードウェア ID は、次のとおりです。 このハードウェア ID の形式は、PCI\\いう<em>v(4)</em>& dev _<em>d(4)</em>& SUBSYS_*s(4)n(4) します。*

    PCI\\VEN_102C&DEV_00E0&SUBSYS_00000000

**注**Windows 10 では、以前のハードウェア Id の一覧で今すぐに表示されるいくつかの Id は、互換性 Id の一覧に表示されます。

## <a name="reporting-compatible-ids"></a>レポートの互換性 Id

次は、PCI バス ドライバーは互換性のある Id を使用して、デバイスの識別文字列形式の一覧です。 これらの形式のさまざまなは、互換性 Id を指定する十分な柔軟性を提供します。 PCI バス ドライバーは、ドライバーは、デバイスから入手できる情報に基づいて互換性 Id の一覧を構築します。 PnP マネージャーでは、デバイスの互換性のある id、ドライバーをクエリ、PCI バス ドライバーは互換性が高い順で互換 Id の一覧を返します。

```cpp
PCI\\VEN_v(4)&DEV_d(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)

PCI\\VEN_v(4)&CC_c(2)s(2)p(2)

PCI\\VEN_v(4)&CC_c(2)s(2)

PCI\\VEN_v(4)

PCI\\CC_c(2)s(2)p(2)&DT_d(4) (applies only to a PCI Express device)

PCI\\CC_c(2)s(2)p(2)

PCI\\CC_c(2)s(2)&DT_d(4) (applies only to a PCI Express device)

PCI\\CC_c(2)s(2)\`
```

各項目の意味は次のとおりです。

-   互換性のある ID で、次のフィールドの定義は、ハードウェア ID で使用されている対応するフィールドの定義と同じです*v(4)*、 *r(2)*、 *c(2)*、。*s(2)*、および*p(2)* します。

-   *d(4)* 、dev _ で*d(4)* フィールドは、デバイスの 4 文字のベンダ定義識別子。

-   *d(4)* 、dt _ で*d(4)* フィールドは、PCI Express の技術仕様で指定されている、4 文字のデバイスの種類。

ポータブル コンピューターのディスプレイ アダプターの例では、そのアダプターの INF ファイルに情報の次の互換性のある Id は一致します。

```cpp
PCI\\VEN_102C&DEV_00E0&REV_04

PCI\\VEN_102C&DEV_00E0

PCI\\VEN_102C&DEV_00E0&REV_04&CC_0300

PCI\\VEN_102C&DEV_00E0&CC_030000

PCI\\VEN_102C&DEV_00E0&CC_0300

PCI\\VEN_102C&CC_030000

PCI\\VEN_102C&CC_0300

PCI\\VEN_102C

PCI\\CC_030000

PCI\\CC_0300
```
 

 





