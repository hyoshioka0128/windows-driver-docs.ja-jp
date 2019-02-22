---
title: XPS フィルター
description: XPS フィルター
ms.assetid: dd8044a6-6558-488e-9508-a83718fabb7d
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- モジュール WDK XPSDrv、XPS フィルターを表示します。
- XPS は、WDK XPSDrv をフィルター処理します。
- DllGetClassObject
- WDK XPS をフィルター処理します。
- IPrintPipelineFilter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bba5075a0d09a710cb670e362c21008f513997b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552609"
---
# <a name="xps-filters"></a>XPS フィルター


XPS 印刷パスでは、フィルターは、ドライバーでは、プリンターの印刷データが準備の主な方法です。 Windows Vista より前に、の Microsoft Windows オペレーティング システムのバージョンでは、プリント プロセッサとレンダリングのモジュールは、フィルターの作業を行いました。

XPS のフィルターをエクスポートする DLL は、 [DllGetClassObject](https://go.microsoft.com/fwlink/p/?linkid=123418)と[DllCanUnloadNow](https://go.microsoft.com/fwlink/p/?linkid=123419)関数。 フィルター パイプライン マネージャーは、スクリプトが読み込まれ、XPS フィルター DLL をアンロードするときに、これらの関数を呼び出します。 フィルターの DLL を読み込んだ後、フィルター パイプライン マネージャーは、次の。

-   呼び出し**DllGetClassObject**フィルター オブジェクトの参照を取得する[IClassFactory](https://go.microsoft.com/fwlink/p/?linkid=123420)インターフェイス。

-   呼び出し、 [IClassFactory::CreateInstance](https://go.microsoft.com/fwlink/p/?linkid=123421)メソッドは、フィルター オブジェクトへの参照を取得する[IPrintPipelineFilter](https://msdn.microsoft.com/library/windows/hardware/ff554286)インターフェイス。

-   呼び出し、 [ **IPrintPipelineFilter::InitializeFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff554291)フィルター オブジェクトを初期化します。

フィルターの DLL をアンロードする前に、フィルター パイプラインの manager 呼び出し**DllCanUnloadNow**します。

**注**  一部の古い XPS フィルターで、 **DllGetClassObject**関数は、フィルターへの参照を取得**IPrintPipelineFilter**の代わりに、インターフェイス**IClassFactory**インターフェイス。 旧バージョンとの互換性のために、これらのフィルターをサポートするために Windows Vista 以降のバージョンの Windows でフィルタ パイプライン マネージャは引き続きします。 ただし、新しいフィルター デザインの**DllGetClassObject**への参照を取得する必要があります、 **IClassFactory**インターフェイス。



XPS フィルターことに印刷サブシステムより堅牢なフィルターが、スプーラーから別のプロセスで実行されるため。 この「サンド ボックス」は、障害から保護し、異なるセキュリティ アクセス許可で実行するプラグインを使用します。 XPSDrv では、コストと開発にかかる時間を削減するプリンターのファミリでフィルターを再利用することもできます。

最大限の柔軟性と再利用の場合は、各フィルターは、特定の印刷処理機能を実行する必要があります。 たとえば、1 つのフィルターだけに適用、透かしアカウンティング別だけ実行中にします。

Windows Vista では、フィルターのボックスは含まれませんで Windows Driver Kit (WDK) で、次のサンプル フィルターが含まれて、 \\Src\\印刷\\Xpsdrvsmpl\\Src\\フィルター フォルダー。

-   小冊子

-   色の変換

-   後処理

-   ページのスケーリング

-   基準値

フィルター パイプライン マネージャーの詳細については、次を参照してください。 [XPSDrv レンダリング モジュール](xpsdrv-render-module.md)します。

フィルターの実装の詳細については、次を参照してください。 [XPS フィルターを実装する](implementing-xps-filters.md)します。

印刷フィルターで非同期通知の詳細については、次を参照してください。[印刷フィルターで非同期通知](asynchronous-notifications-in-print-filters.md)します。

使用してフィルターを構成する必要があります、[フィルター パイプライン構成ファイル](filter-pipeline-configuration-file.md)します。

印刷フィルター パイプラインのサービスをデバッグする方法については、次を参照してください。[フィルター パイプラインの印刷サービスにデバッガーをアタッチ](attaching-a-debugger-to-the-print-filter-pipeline-service.md)します。

Windows 7、XPS フィルターを使用できます、 [XPS ラスタライズ サービス](using-the-xps-rasterization-service.md)ビットマップに XPS ドキュメントのページを固定に変換します。

XPS ラスタライズの GPU アクセラレータを使用する Windows の方法についてを参照してください。 [XPSRas GPU 利用デシジョン ツリー](xpsras-usage-decision-tree.md)します。

