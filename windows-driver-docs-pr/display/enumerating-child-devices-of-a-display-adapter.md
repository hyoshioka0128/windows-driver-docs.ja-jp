---
title: ディスプレイ アダプターの子デバイスの列挙
description: ディスプレイ アダプターの子デバイスの列挙
ms.assetid: 3bec2117-aef4-41fc-b88a-0081c7c9fe3d
keywords:
- ビデオの WDK 表示のネットワークを表示、アダプター子デバイスを表示します。
- VidPN WDK の表示、ディスプレイ アダプター子デバイス
- 子デバイス WDK ビデオ存在するネットワーク
- アダプター子デバイス WDK ビデオ存在するネットワークを表示します。
- 子デバイス WDK ビデオ存在するネットワークを列挙します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 829713c12927b7a9d544f107f8902d78a42c1868
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377658"
---
# <a name="enumerating-child-devices-of-a-display-adapter"></a>ディスプレイ アダプターの子デバイスの列挙


次の一連の手順では、ポートのディスプレイ ドライバー、ディスプレイのミニポート ドライバー、およびビデオの表示 (VidPN) のネットワーク マネージャーが列挙子デバイス ディスプレイ アダプターの初期化時に共同作業する方法について説明します。

1.  ポートのディスプレイ ドライバー呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiStartDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560775)関数。 *DxgkDdiStartDevice*を返します (で、*コード*パラメーター) が (またはドッキングなる可能性があります) をデバイスの数、ディスプレイ アダプターの子。 *DxgkDdiStartDevice*も返されます (で、 *NumberOfVideoPresentSources*パラメーター) ディスプレイ アダプターでサポートされているビデオの存在するソースの数を N。 これらのビデオの存在するソースは、その後数字 0、1、によって識別される.N は-1。

2.  ポートのディスプレイ ドライバー呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiQueryChildRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff559750)関数で、子のデバイスのディスプレイ アダプターを列挙します。 *DxgkDdiQueryChildRelations*の配列に格納[ **DXGK\_子\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff561001)構造: 子デバイスごとに 1 つ。 ディスプレイ アダプターのすべての子デバイスがオンボードことに注意してください: モニター ディスプレイ アダプターに接続するその他の外部デバイスでは、子デバイスを考慮はされません。 詳細については、次を参照してください。[ディスプレイ アダプターの子デバイス](child-devices-of-the-display-adapter.md)します。 *DxgkDdiQueryChildRelations*潜在的な子デバイスだけではなく、初期化時に物理的に存在する子デバイスを列挙する必要があります。 たとえばをドッキングするラップトップ コンピューターを接続する場合ステーションが新しいのビデオ出力の外観の結果は*DxgkDdiQueryChildRelations*ビデオ出力かどうかに関係なく、コンピューターがドッキングされるを列挙する必要があります初期化時間です。 ドングルをビデオ出力コネクタに接続する場合は、コネクタを共有する複数のモニターを許可また、 *DxgkDdiQueryChildRelations*ドングルが表示されるかどうかに関係なく、ドングルの各分岐の子デバイスを列挙する必要があります初期化時に接続します。

3.  デバイスごとに子 (手順 1. で説明したよう列挙型) の HPD 認識値を持つ**HpdAwarenessInterruptible**または**HpdAwarenessPolled**ポートのディスプレイ ドライバーが表示ミニポートを呼び出すドライバーの[ **DxgkDdiQueryChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559754)子デバイスに接続されている外部デバイスがあるかどうかを判断する関数。

4.  ポートのディスプレイ ドライバーを次の条件のいずれかを満たす子デバイスごとの PDO を作成します。
    -   子デバイス HPD 認識価値がある**HpdAwarenessAlwaysConnected**します。
    -   子デバイス HPD 認識価値がある**HpdAwarenessPolled**または**HpdAwarenessInterruptible**、前のクエリや子デバイスがあるという通知から、オペレーティング システムを知っていると、外部デバイスが接続されています。

5.  ポートのディスプレイ ドライバー呼び出しディスプレイ ミニポート ドライバーの[ **DxgkDdiQueryDeviceDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff559761)関数を次の条件のいずれかを満たす子デバイスごとに。

    -   子デバイスは、外部デバイスが接続されているが知られています。
    -   子デバイスは、外部デバイスが接続されていると見なされます。
    -   子デバイスの種類を持つ**TypeOther**します。

    *DxgkDdiQueryDeviceDescriptor*接続されているモニター (またはその他のディスプレイ デバイス) は EDID 記述子をサポートしている場合は、拡張表示情報 Data (EDID) ブロックを返します。

    注:ポートのディスプレイ ドライバーが呼び出して初期化中に、 *DxgkDdiQueryDeviceDescriptor*モニターのディスプレイが EDID の最初の 128 バイトのブロックを取得するモニターごとにします。 により、ポートのディスプレイ ドライバーの初期化時に必要なもの。プラグ アンド プレイ ハードウェア ID、インスタンス ID、互換性 Id、およびデバイスのテキスト。 モニター クラス関数ドライバー (Monitor.sys) の呼び出しは後で*DxgkDdiQueryDeviceDescriptor*の最初の 128 バイト EDID ブロックと 128 バイト EDID 拡張機能の追加のブロックを取得するには、各モニター。 これは、ディスプレイのミニポート ドライバーが各モニターのディスプレイが EDID の最初の 128 バイトのブロックを提供するには、2 回呼び出されることを意味します。

6.  VidPN マネージャーは、存在するソースのビデオとディスプレイ アダプターでサポートされているビデオの存在ターゲットのすべての識別子を取得します。 ビデオのあるソースは、数値 0, 1, によって識別されます.N-1、N はソースの表示のミニポート ドライバーによって返される数*DxgkDdiStartDevice*関数。 ビデオの存在ターゲット中にディスプレイのミニポート ドライバーによって以前に作成された一意の整数識別子がある*DxgkDdiQueryChildRelations*します。 型の場合は、各子デバイス**TypeVideoOutput**ビデオの存在ターゲットに関連付けられた、 **ChildUid**メンバーの子デバイスの DXGK\_子\_記述子構造体ビデオの存在ターゲットの識別子として使用されます。

7.  VidPN マネージャーは、初期の VidPN を構築するのに、次の手順を使用します。
    -   最後の既知の適切な VidPN はレジストリに記録されて、いる場合は、初期 VidPN として使用します。

    -   それ以外の場合、ディスプレイのミニポート ドライバーを呼び出す[ **DxgkDdiRecommendFunctionalVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559775)初期の VidPN を取得します。

    -   場合*DxgkDdiRecommendFunctionalVidPn*失敗を許容できますが、ある機能 VidPN を返す単純な VidPN 1 つのビデオの表示パスを格納している。 つまり、(ソース、ターゲット) のいずれかのペアを作成します。 呼び出すディスプレイ ミニポート ドライバーの[ **DxgkDdiIsSupportedVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559684)提案 VidPN が動作することを確認する関数。 場合*DxgkDdiIsSupportedVidPn*に適した VidPN が見つかるまで、提案された VidPN が動作しないレポートを続けます。

    -   呼び出すディスプレイ ミニポート ドライバーの[ **DxgkDdiEnumVidPnCofuncModality** ](https://msdn.microsoft.com/library/windows/hardware/ff559649) VidPN で利用可能なソースとターゲットのモードを決定する関数。

 

 





