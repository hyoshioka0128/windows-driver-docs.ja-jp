---
title: XPS フィルター
description: XPS フィルター
ms.assetid: dd8044a6-6558-488e-9508-a83718fabb7d
keywords:
- XPSDrv プリンタードライバー WDK、render モジュール
- レンダーモジュール WDK XPSDrv、XPS フィルター
- XPS フィルター WDK XPSDrv
- DllGetClassObject
- WDK XPS をフィルター処理します
- IPrintPipelineFilter
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 64169a01f28736f62785c02bf5f910ec37e0719b
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793742"
---
# <a name="xps-filters"></a>XPS フィルター

XPS 印刷パスでは、ドライバーがプリンターの印刷データを準備する主な方法としてフィルターが使用されます。 Windows Vista より前のバージョンの Microsoft Windows オペレーティングシステムでは、プリントプロセッサとレンダリングモジュールによってフィルター処理が行われました。

XPS フィルターは、 [DllGetClassObject](https://go.microsoft.com/fwlink/p/?linkid=123418)関数と[DllCanUnloadNow](https://go.microsoft.com/fwlink/p/?linkid=123419)関数をエクスポートする DLL です。 フィルターパイプラインマネージャーは、XPS フィルター DLL を読み込んでアンロードするときに、これらの関数を呼び出します。 フィルターの DLL を読み込むと、フィルターパイプラインマネージャーは次の処理を実行します。

- **DllGetClassObject**を呼び出して、フィルターオブジェクトの[IClassFactory](https://go.microsoft.com/fwlink/p/?linkid=123420)インターフェイスへの参照を取得します。

- [IClassFactory:: CreateInstance](https://go.microsoft.com/fwlink/p/?linkid=123421)メソッドを呼び出して、フィルターオブジェクトの[iprintpipelinefilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinefilter)インターフェイスへの参照を取得します。

- [**Iprintpipelinefilter:: initializefilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)メソッドを呼び出して、フィルターオブジェクトを初期化します。

フィルター DLL をアンロードする前に、フィルターパイプラインマネージャーは**DllCanUnloadNow**を呼び出します。

> [!NOTE]
> 一部の古い XPS フィルターでは、 **DllGetClassObject**関数は、 **IClassFactory**インターフェイスではなく、フィルターの**iprintpipelinefilter**インターフェイスへの参照を取得します。 旧バージョンとの互換性のために、Windows Vista 以降のバージョンの Windows のフィルターパイプラインマネージャーでは、これらのフィルターが引き続きサポートされます。 ただし、新しいフィルターデザインの場合、 **DllGetClassObject**は**IClassFactory**インターフェイスへの参照を取得する必要があります。

XPS フィルターを使用すると、印刷サブシステムの堅牢性が向上します。これは、フィルターがスプーラとは異なるプロセスで実行されるためです。 この "サンドボックス" は、エラーから保護し、別のセキュリティアクセス許可でプラグインを実行できるようにします。 また、XPSDrv を使用すると、複数のプリンターにわたるフィルターを再利用して、コストと開発時間を削減することもできます。

柔軟性を最大限に高め、再利用するには、各フィルターが特定の印刷処理機能を実行する必要があります。 たとえば、1つのフィルターではウォーターマークのみが適用され、別のフィルターではアカウンティングのみが実行されます。

Github では、次の[XPS ドライバーとフィルターのサンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/xpsdrv-driver-and-filter-sample/)を入手できます。

- [製本する]

- カラー変換

- Nup

- ページのスケーリング

- ウォーターマーク

フィルターパイプラインマネージャーの詳細については、「 [XPSDrv Render Module](xpsdrv-render-module.md)」を参照してください。

フィルターの実装の詳細については、「 [XPS フィルターの実装](implementing-xps-filters.md)」を参照してください。

印刷フィルターでの非同期通知の詳細については、「[印刷フィルターでの非同期通知](asynchronous-notifications-in-print-filters.md)」を参照してください。

フィルター[パイプライン構成ファイル](filter-pipeline-configuration-file.md)を使用してフィルターを構成する必要があります。

印刷フィルターパイプラインサービスをデバッグする方法の詳細については、「[印刷フィルターパイプラインサービスへのデバッガーのアタッチ](attaching-a-debugger-to-the-print-filter-pipeline-service.md)」を参照してください。

Windows 7 では、xps フィルターは xps[ラスタライズサービス](using-the-xps-rasterization-service.md)を使用して xps ドキュメント内の固定ページをビットマップに変換できます。

Windows が XPS ラスタライズに GPU アクセラレーションを使用する方法の詳細については、「azure [Gpu 使用率のデシジョンツリー](xpsras-usage-decision-tree.md)」を参照してください。
