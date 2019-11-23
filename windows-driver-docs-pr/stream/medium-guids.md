---
title: メディアの GUID
description: メディアの GUID
ms.assetid: 4209952c-0ba5-4359-b612-91529a0a46f1
keywords:
- ビデオキャプチャ WDK AVStream、メディア
- ビデオのキャプチャ WDK AVStream、メディア
- メディア WDK ビデオキャプチャ
- ピン接続の WDK ビデオキャプチャ
- Guid WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e15b7a2bb052fd8b31789a122d94b7a1cb8dbadb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838040"
---
# <a name="medium-guids"></a>メディアの GUID


ミニドライバーは、複数のデバイスをサポートできる必要があります。 さらに、テレビ/ラジオチューナー、テレビオーディオ、クロスバー、およびビデオキャプチャのコンポーネントが異なるカーネルストリーミングフィルターに分割されているため、次のコンポーネント間のトポロジハードウェア接続を正しく記述する必要があります。デバイスに加えて、複数のデバイスにも対応します。 たとえば、FM ラジオとテレビキャプチャをサポートする、2つのビルドされたが実行されていないフィルターグラフは、共存させることができなければなりません。 ミニドライバーは、これらのシナリオに対応するためにメディアを使用します。 また、*グラフの編集*などのフィルターグラフ作成アプリケーションでは、フィルターグラフの構築時にメディアを使用して、あるデバイスのフィルターが別のデバイスのフィルターに正しく接続されるようにします。 たとえば、あるデバイスのチューナーフィルターでは、別のデバイスのクロスバーフィルターに接続することはできません。

ミニドライバーは、GUID データ型のメンバー (**セット**) と2つの ULONG メンバー (**Id**と**フラグ**) で構成される[**kspin\_MEDIUM**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))構造のメディアについて説明します。

-   **Set**メンバーには、トポロジハードウェア接続を表す GUID を割り当てる必要があります。

-   ミニドライバーでは、 **Id**メンバーをデバイスインスタンスの一意の値に設定する必要があります。

-   **Flags**メンバーはシステム使用のために予約されており、0に設定する必要があります。

システム内に複数のデバイスを含むフィルターグラフを適切に構築するために、KSPIN\_MEDIUM 構造体の**セット**メンバーは、各デバイスインスタンスで同じままです。 ただし、ミニドライバーでは、デバイスインスタンスごとに KSPIN\_MEDIUM 構造の**Id**メンバーに一意の値を割り当てる必要があります。 **Id**メンバーを一意の値に設定できないと、システムに複数のデバイスが存在する場合に問題が発生します。 2つのデバイスがシステムにインストールされている場合、ミニドライバーは、デバイスインスタンスごとに**Id**メンバーを別の値に設定する必要があります。 チューナーやクロスバーなど、同じハードウェア上にあるデバイスのフィルターの**Id**メンバーは同じであることに注意してください。 **Id**メンバーがデバイスインスタンス間で異なることを保証する方法の1つは、 **id**を値に設定する前に、ミニドライバーにグローバルカウンターを設定し、デバイスプラグアンドプレイの開始時刻にそのカウンターをインクリメントすることです。

ミニドライバーが従うカーネルストリーミングインターフェイス (AVStream または Stream クラス) に応じて、ミニドライバーは**Id**メンバーの値を別の方法で指定する必要があります。

-   Stream クラスミニドライバーを処理するときに値を指定し[ **\_ストリーム\_情報を取得\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)ます。

-   AVStream ミニドライバー [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の値を指定します。 AVStream ミニドライバーには、KSPIN\_記述子\_EX 構造体の値を指定する2つの異なる方法があります。

    1.  グローバル**id**カウンターを使用して静的な記述子を指定し、 *Add*または*Start*ディスパッチハンドラーで[**KsEdit を\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit)呼び出して**Id**メンバーを一意の値に変更します。
    2.  [**KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory)を呼び出して、 *Add*または*Start*ディスパッチハンドラーの間にフィルター/ピン記述子を動的に構築します。

また、ミニドライバーは、Microsoft DirectShow に登録する特別な関数を呼び出す必要があります。これにより、アプリケーションは実際には作成されないため、テレビ/ラジオチューナー、テレビオーディオ、およびクロスバーフィルターを使用してフィルターグラフを自動的に作成することができます。入力と出力のためのカーネルストリーミングピン。 ミニドライバーがこれらのフィルターを登録すると、KSPIN\_中構造体の**Id**メンバーが一意の値に設定されます。 ミニドライバーが KSPIN\_MEDIUM 構造体の**Id**メンバーを一意の値に設定していない場合、graph の自動構築アプリケーションは、必要な隣接するフィルターの読み込みに失敗する可能性があります。 ただし、たとえば、グラフの編集では、手動フィルター (グラフの作成) が引き続き機能する場合があります。

ミニドライバーを DirectShow に登録するには:

-   Stream クラスミニドライバーは、 [**StreamClassRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisterfilterwithnokspins)関数を呼び出して、フィルターを DirectShow に登録します。

-   AVStream ミニドライバー [**KsRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksregisterfilterwithnokspins)関数を呼び出して、フィルターを DirectShow に登録します。

-   または、ミニドライバーが BDA モデルに従っており、特定の[**Ksfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)構造の下にある特定の[**KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造の複数のインスタンスが同じカーネルストリーミングカテゴリに登録されている場合は、 [**KsFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterfactoryupdatecachedata) (または[**BdaFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdafilterfactoryupdatecachedata)) 関数を呼び出して、フィルターを DirectShow に登録します。

SRB\_GET\_STREAM\_INFO (Stream クラスミニドライバーの場合)、または KSPIN\_DESCRIPTOR\_EX (AVStream ミニドライバーの場合) から返される KSPIN\_MEDIUM 構造体は、次のプロパティで返される KSPIN\_MEDIUM メンバーと一致する必要があります。

-   Ksk プロパティの**Medium**メンバーは、 [**KSK プロパティ\_クロスバー\_pininfo**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo)の[ **\_クロスバー\_pininfo\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)構造体を持ちます。 メディアが一致しない場合、グラフの作成はミニドライバーのフィルターとグラフ内の隣接するフィルターの間で失敗する可能性があります。

-   Ksk プロパティ\_チューナーの**videomedium**メンバーと**audiomedium**メンバーは、 [ **\_caps\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)構造体の[**ksk プロパティ\_チューナー\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-caps)を持ちます。

-   Ksk プロパティの**inputmedium**メンバーと**outputmedium**メンバー\_、 [**TVAUDIO\_Caps**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-caps)の[ **\_caps\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s)構造体を\_します。

メディアとメディアの Guid を正しく実装するだけでなく、プロセスが複数のフィルターグラフで動作することを確認するために、他のガイドラインに従う必要があります。 ミニドライバーは、フィルターグラフが**Ksk 状態**に遷移するまで、ハードウェアリソースをロックしないようにする必要があります。この場合\_ksk 状態の値を取得します。 これにより、2つのビルドされた (ただし、実行されていない) フィルターグラフを相互に干渉することなく共存させることができます。

メディアの実装方法など、メディアの詳細については、 [Avstream のシミュレートされたハードウェアサンプルドライバー (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)に関する説明を参照してください。

**注**  : Windows Driver Kit のサンプルコードから新しいミニドライバーを派生させる場合は、デバイスの一意のハードウェアトポロジを反映するために、メディアの新しい GUID 値を生成する必要があります。 そうしないと、別のデバイスに対して定義されているメディアと1つのデバイスのメディアが衝突する可能性があります。

 

 

 




