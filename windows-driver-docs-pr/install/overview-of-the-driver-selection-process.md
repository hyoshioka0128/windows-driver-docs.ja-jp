---
title: ドライバーの選択プロセスの概要
description: ドライバーの選択プロセスの概要
ms.assetid: 120ab9f9-6ac5-4b76-bee1-2e975d0c38f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a43355c0238b8b73223cbcaaef7117203526e0e
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557738"
---
# <a name="overview-of-the-driver-selection-process"></a>ドライバーの選択プロセスの概要


Windows は、ドライバーを*ドライバーノード*として表します。これには、サービス、デバイス固有の共同インストーラー、レジストリエントリなど、デバイスのすべてのソフトウェアサポートが含まれます。 デバイスのサービスには、関数ドライバーと、上位レベルおよび低レベルのデバイスフィルタードライバーが含まれます。

一部のデバイスでは、ベンダーが提供するドライバーが必要です。このドライバーは、そのデバイス専用に設計されているか、デバイスファミリをサポートするように設計されています。 ただし、その他のデバイスは、特定の[デバイスセットアップクラス](device-setup-classes.md)のすべてのデバイスをサポートするシステム提供のドライバーによって駆動されます。 Windows は、デバイスに最も近いドライバーを選択します。 このようなドライバーが見つからない場合は、より多くの一般的なドライバーを選択します。

### <a name="how-windows-searches-for-drivers"></a><a href="" id="how-setup-searches-for-drivers"></a>Windows でのドライバーの検索方法

Windows は、特定の場所で、デバイスに一致するドライバーを検索します。 次の条件に該当する場合、ドライバーはデバイスと一致します。

-   デバイスのバスドライバーによって報告されたプラグアンドプレイ (PnP)[デバイス識別文字列](device-identification-strings.md)の1つは、ドライバーの[inf ファイル](overview-of-inf-files.md)の " [**inf*モデル*" セクション**](inf-models-section.md)エントリのデバイス識別文字列と一致します。

-   [**INF*モデル*セクション**](inf-models-section.md)エントリの一致するデバイス id 文字列で*TargetOSVersion*装飾が指定されている場合、そのデコレーションは、デバイスをインストールするオペレーティングシステムのバージョンと一致します。

    *TargetOSVersion*装飾の詳細については、「[プラットフォーム拡張機能とオペレーティングシステムバージョンの組み合わせ](combining-platform-extensions-with-operating-system-versions.md)」を参照してください。

Windows が一致するドライバーを検索する場所の詳細については、「 [windows がドライバーを検索する場所](where-setup-searches-for-drivers.md)」を参照してください。

### <a name="how-windows-ranks-drivers"></a><a href="" id="how-setup-ranks-drivers"></a>Windows がドライバーをランク付けする方法

一致するすべてのドライバーの一覧が作成され、各ドライバーにランクが割り当てられます。 Windows は、各ドライバーのランクを0以上の整数値で表します。

順位付けプロセスの詳細については、「 [Windows がドライバーをランク付けする方法](how-setup-ranks-drivers--windows-vista-and-later-.md)」を参照してください。

Windows Vista 以降では、ドライバーがデジタル署名されているかどうかに基づいてドライバーもランク付けされます。 Windows は、次のように、デジタル署名に基づいてドライバーをランク付けします。

-   [ **AllSignersEqual**グループポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)が無効になっている場合、Windows は、 [Authenticode](authenticode.md)署名で署名されたドライバーよりも高い Microsoft 署名で署名されたドライバーをランク付けします。 この順位付けは、Authenticode 署名で署名されたドライバーが、その他のすべての側面でデバイスに対してより適切に一致している場合でも発生します。

-   [ **AllSignersEqual**グループポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)が有効になっている場合、Windows はデジタル署名されたすべてのドライバーを均等にランク付けします。

**メモ**   Windows 7 以降では、 [AllSignersEqual グループポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)が既定で有効になっています。 Windows Vista および Windows Server 2008 では、 **AllSignersEqual**グループポリシーは既定で無効になっています。 IT 部門は、 **AllSignersEqual**グループポリシーを有効または無効にすることで、既定の順位付け動作を上書きできます。

 

Windows 署名機関からの署名には、次のものが含まれます。

-   Premium Windows Hardware Quality Labs (WHQL) の署名と標準の WHQL 署名

-   受信トレイドライバーの署名

-   Windows の継続的エンジニアリング (Windows SE) の署名

-   ドライバーのデバイスセットアップクラスの[LowerLogoVersion](lowerlogoversion.md)値と同じかそれ以降の Windows バージョンの WHQL 署名

### <a name="how-windows-selects-drivers"></a><a href="" id="how-setup-selects-drivers"></a>Windows がドライバーを選択する方法

デバイスに最適なランク値を持つドライバーが、Windows によって選択されます。

ただし、デバイスに最適な一致のドライバーが複数ある場合、Windows はドライバーの日付とバージョンを使用してドライバーを選択します。 ドライバーの日付とバージョンは、ドライバーの[inf ファイル](overview-of-inf-files.md)に格納されている[**inf DriverVer ディレクティブ**](inf-driverver-directive.md)によって指定されます。

Windows では、デバイスのドライバーを選択するために次の条件を使用します。

-   デバイスに最適なランク値を持つドライバーが、Windows によって選択されます。

-   ランクが等しいドライバーの場合、Windows は最新の日付を持つドライバーを選択します。

-   ランクと日付が等しいドライバーの場合、Windows は最も高いバージョンのドライバーを選択します。

-   ランク、日付、およびバージョンが同じドライバーの場合、Windows は任意のドライバーを選択できます。

 

 





