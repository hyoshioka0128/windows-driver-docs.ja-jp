---
title: ドライバーの選択プロセスの概要
description: ドライバーの選択プロセスの概要
ms.assetid: 120ab9f9-6ac5-4b76-bee1-2e975d0c38f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d154e17f867200696eb190a175b257daa70058
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388302"
---
# <a name="overview-of-the-driver-selection-process"></a>ドライバーの選択プロセスの概要


Windows ドライバーとしてを表す、*ドライバー ノード*、任意のサービス、デバイスに固有の共同インストーラー、およびレジストリ エントリなど、デバイスのすべてのソフトウェアのサポートが含まれています。 デバイスのサービスには、関数のドライバーと、デバイス上のレベルと下位レベルのフィルター ドライバーが含まれます。

一部のデバイスでは、そのデバイスまたはデバイスのファミリをサポートするように設計されたいずれか専用のように設計されたベンダーから提供されたドライバーが必要です。 すべてのデバイスをサポートするシステム提供のドライバーによって他のデバイスを実行できますを指定した[デバイス セットアップ クラス](device-setup-classes.md)します。 Windows では、デバイスに最も一致するドライバーを選択します。 このようなドライバーが見つからない場合は、Windows の場合は、ますます一般的なドライバーから選択します。

### <a href="" id="how-setup-searches-for-drivers"></a> Windows でドライバーを検索する方法

Windows デバイスと一致するドライバーの特定の場所を検索します。 ドライバーでは、次の場合、デバイスが一致します。

-   プラグ アンド プレイ (PnP) のいずれかの[識別文字列](device-identification-strings.md)デバイスとデバイスの識別文字列が一致するバス ドライバーによって報告された、 [ **INF*モデル*セクション**](inf-models-section.md)エントリのドライバーの[INF ファイル](inf-files.md)します。

-   一致するデバイス id の文字列の場合、 [ **INF*モデル*セクション**](inf-models-section.md)エントリを指定します、 *TargetOSVersion*装飾、装飾では、デバイスのインストールをオペレーティング システムのバージョンと一致します。

    詳細については、 *TargetOSVersion*の装飾を参照してください[プラットフォーム拡張機能バージョンのオペレーティング システムと組み合わせて](combining-platform-extensions-with-operating-system-versions.md)します。

Windows のドライバーの一致を検索する場所の詳細については、次を参照してください。[ドライバーが Windows 検索](where-setup-searches-for-drivers.md)します。

### <a href="" id="how-setup-ranks-drivers"></a> Windows ドライバーをランク付けする方法

Windows では、一致するすべてのドライバーの一覧を作成し、各ドライバーのランクを割り当てます。 Windows より大きいまたは 0 以下である整数値を持つ各ドライバーのランクを表します。

順位付けのプロセスの詳細については、次を参照してください。[ランク ドライバーをどのように Windows](how-setup-ranks-drivers.md)します。

Windows Vista 以降、Windows をランク付けしてドライバーをドライバーがデジタル署名されているかどうかに基づいています。 Windows には、次のようにデジタル署名に基づいたドライバーが順位付けされます。

-   場合、 [ **AllSignersEqual**グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)は Windows ランク付けを無効になっている、マイクロソフトの署名で署名されたドライバーよりも高いで署名されたドライバー、 [Authenticode](authenticode.md)署名します。 この順位付けは、Authenticode 署名で署名されたドライバーは、その他のすべての面で、デバイスに適している場合でも発生します。

-   場合、 [ **AllSignersEqual**グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)が有効にすると、Windows をランク付けデジタル署名されたドライバーをすべて均等にします。

**注**  以降、Windows 7 で、 [AllSignersEqual グループ ポリシー](allsignersequal-group-policy--windows-vista-and-later-.md)既定で有効です。 Windows Vista および Windows Server 2008、 **AllSignersEqual**グループ ポリシーが既定で無効になっています。 IT 部門は、既定の動作を有効または無効に順位付けをオーバーライドできます、 **AllSignersEqual**グループ ポリシー。

 

署名機関を Windows からの署名を以下に示します。

-   Premium Windows Hardware Quality Labs (WHQL) の署名と標準 WHQL 署名

-   受信トレイのドライバーの署名

-   Windows Sustained Engineering (Windows SE) の署名

-   同じである Windows バージョンについては、WHQL 署名かそれより遅い、 [LowerLogoVersion](lowerlogoversion.md)ドライバーのデバイス セットアップ クラスの値

### <a href="" id="how-setup-selects-drivers"></a> Windows ドライバーを選択する方法

Windows では、デバイスに最適なものとして、ドライバーを最低ランク値を選択します。

ただしはデバイスの最適な一致する複数の均等にランク付けされたドライバーがある場合は、Windows を使用して、ドライバーの日付とバージョン ドライバーを選択します。 ドライバーの日付とバージョンがで指定された、 [ **INF DriverVer ディレクティブ**](inf-driverver-directive.md)に含まれるドライバーの[INF ファイル](inf-files.md)します。

Windows は、次の条件を使用し、デバイスのドライバーを選択します。

-   Windows では、デバイスに最適なものとして最も低い順位値を持つドライバーを選択します。

-   ランクが等しいドライバーでは、Windows はドライバーが最新の日付を選択します。

-   ランクが等しいと日付を持つドライバーについては、Windows は、最上位のバージョンのあるドライバーを選択します。

-   ランクが等しい、日付、およびバージョンのあるドライバーは、Windows は、すべてのドライバーを選択できます。

 

 





