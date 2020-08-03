---
title: PCI デバイスの識別子
description: PCI デバイスの識別子
ms.assetid: 58d52af8-9afd-441f-9ed9-92f9e2775226
keywords:
- デバイス識別文字列 WDK、PCI デバイス
- id 文字列 WDK デバイス、PCI デバイス
- id WDK デバイス、PCI デバイス
- PCI デバイス識別子 WDK デバイスのインストール
- ハードウェア Id WDK デバイスのインストール
- 互換性 Id WDK デバイスのインストール
ms.date: 05/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1da5bb7750b2a8a24e322faf6a705fb80d987fb3
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473760"
---
# <a name="identifiers-for-pci-devices"></a>PCI デバイスの識別子

> [!IMPORTANT]
> Pci デバイスで使用されている既知の Id の一覧については、 [PCI ID リポジトリ](https://pci-ids.ucw.cz/)を参照してください。 Windows の Id を一覧表示するには、を使用 `devcon hwids *` します。

次に示すのは、PCI バスドライバーがハードウェア Id を報告するために使用する[デバイス id 文字列](device-identification-strings.md)形式の一覧です。 プラグアンドプレイ (PnP) マネージャーが、デバイスのハードウェア Id のドライバーに対してクエリを行うと、PCI バスドライバーは一般性が増加する順にハードウェア Id の一覧を返します。

```cpp
PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)

PCI\\VEN_v(4)&DEV_d(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)p(2)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)
```

この場合、

- v (4) は、デバイスのベンダーに対して、4文字の PCI SIG で割り当てられた識別子です。 PCI SIG usage の後の*デバイス*という用語は、特定の pci チップを指します。

- d (4) は、デバイスの4文字のベンダー定義識別子です。

- s (4) は、4文字のベンダー定義サブシステム識別子です。

- n (4) は、サブシステムのベンダーに対して、4文字の PCI SIG で割り当てられた識別子です。

- r (2) は2文字のリビジョン番号です。

- c (2) は、構成領域からの2文字の基本クラスコードです。

- s (2) は、2文字のサブクラスコードです。

- p (2) はプログラミングインターフェイスコードです。

ポータブルコンピューターのディスプレイアダプターのハードウェア ID の例を次に示します。 このハードウェア ID の形式は PCI \\ VEN_v (4) &DEV_d (4) &SUBSYS_s (4) n (4) &REV_r (2):

`PCI\\VEN_102C&DEV_00E0&SUBSYS_00000000&REV_04`

次に示すのは、前の例のディスプレイアダプターのハードウェア ID で、リビジョン情報が削除されたものです。 このハードウェア ID の形式は、PCI \\ VEN_<em>v (4)</em>&DEV_<em>d (4</em> )&SUBSYS_*s (4) n (4) です。*

`PCI\\VEN_102C&DEV_00E0&SUBSYS_00000000`

>[!NOTE]
>Windows 10 では、以前にハードウェア Id の一覧に表示されていた Id の一部が互換性 Id の一覧に表示されるようになりました。

## <a name="reporting-compatible-ids"></a>互換性 Id のレポート

次に示すのは、PCI バスドライバーが互換性 Id を報告するために使用するデバイス id 文字列形式の一覧です。 これらの形式のさまざまな機能により、互換性のある Id を柔軟に指定できます。 PCI バスドライバーは、ドライバーがデバイスから取得できる情報に基づいて、互換性のある Id の一覧を構築します。 PnP マネージャーがデバイスの互換性のある Id をドライバーに照会すると、PCI バスドライバーは互換性のために互換性のある Id の一覧を返します。

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

この場合、

- 互換性のある id の次のフィールドの定義は、ハードウェア ID: *v (4)*、 *r (2)*、 *c (2)*、 *s (2*)、および*p (2*) で使用される、対応するフィールドの定義と同じです。

- DEV_*d (4)* フィールドの*d (4)* は、デバイスの4文字のベンダー定義識別子です。

- DT_*d (4)* フィールドの*d (4)* は、PCI Express 基本仕様で指定されている4文字のデバイスの種類です。

ポータブルコンピューターのディスプレイアダプターの例では、次の互換性のある Id のいずれかが、そのアダプターの INF ファイルの情報と一致します。

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
