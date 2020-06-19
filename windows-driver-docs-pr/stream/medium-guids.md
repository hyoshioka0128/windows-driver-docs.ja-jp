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
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: b026d2e276006260cb640e20f703b2d4b7814d33
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992469"
---
# <a name="medium-guids"></a>メディアの GUID

ミニドライバーは、複数のデバイスをサポートできる必要があります。 さらに、テレビ/ラジオチューナー、テレビオーディオ、クロスバー、およびビデオキャプチャのコンポーネントが異なるカーネルストリーミングフィルターに分割されているため、デバイス上のこれらのコンポーネントと複数のデバイスの間のトポロジハードウェア接続を正しく記述するためにメソッドが必要です。 たとえば、FM ラジオとテレビキャプチャをサポートする、2つのビルドされたが実行されていないフィルターグラフは、共存させることができなければなりません。 ミニドライバーは、これらのシナリオに対応するためにメディアを使用します。 また、*グラフの編集*などのフィルターグラフ作成アプリケーションでは、フィルターグラフの構築時にメディアを使用して、あるデバイスのフィルターが別のデバイスのフィルターに正しく接続されるようにします。 たとえば、あるデバイスのチューナーフィルターでは、別のデバイスのクロスバーフィルターに接続することはできません。

ミニドライバーは、GUID データ型のメンバー (**セット**) と2つの ULONG メンバー (**Id**と**フラグ**) で構成される[**kspin \_ MEDIUM**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))構造のメディアについて説明します。

- **Set**メンバーには、トポロジハードウェア接続を表す GUID を割り当てる必要があります。

- ミニドライバーでは、 **Id**メンバーをデバイスインスタンスの一意の値に設定する必要があります。

- **Flags**メンバーはシステム使用のために予約されており、0に設定する必要があります。

システムに複数のデバイスを含むフィルターグラフを適切に構築するために、KSPIN MEDIUM 構造体の**セット**メンバーは、 \_ 各デバイスインスタンスで同じままです。 ただし、ミニドライバーは、デバイスインスタンスごとに KSPIN MEDIUM 構造の**Id**メンバーに一意の値を割り当てる必要があり \_ ます。 **Id**メンバーを一意の値に設定できないと、システムに複数のデバイスが存在する場合に問題が発生します。 2つのデバイスがシステムにインストールされている場合、ミニドライバーは、デバイスインスタンスごとに**Id**メンバーを別の値に設定する必要があります。 チューナーやクロスバーなど、同じハードウェア上にあるデバイスのフィルターの**Id**メンバーは同じであることに注意してください。 **Id**メンバーがデバイスインスタンス間で異なることを保証する方法の1つは、 **id**を値に設定する前に、ミニドライバーにグローバルカウンターを設定し、デバイスプラグアンドプレイの開始時刻にそのカウンターをインクリメントすることです。

ミニドライバーが従うカーネルストリーミングインターフェイス (AVStream または Stream クラス) に応じて、ミニドライバーは**Id**メンバーの値を別の方法で指定する必要があります。

- Stream クラスミニドライバー [**SRB の \_ \_ ストリーム \_ 情報の取得**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)を処理するときに値を指定します。

- AVStream ミニドライバー [**Kspin \_ 記述子 \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の値を指定します。 AVStream ミニドライバーには、KSPIN \_ 記述子 EX 構造体の値を指定する2つの異なる方法があり \_ ます。

    1. グローバル**id**カウンターを使用して静的記述子を指定し、 *Add*または*Start*ディスパッチハンドラーで[** \_ KsEdit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit)を呼び出して、 **Id**メンバーを一意の値に変更します。

    1. [**KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory)を呼び出して、 *Add*または*Start*ディスパッチハンドラーの間にフィルター/ピン記述子を動的に構築します。

また、ミニドライバーは、Microsoft DirectShow に登録するための特別な関数を呼び出す必要があります。これにより、アプリケーションは、入力と出力に対して実際にはカーネルストリーミング pin を作成しないため、テレビ/ラジオチューナー、テレビオーディオ、およびクロスバーフィルターを使用してフィルターグラフを自動的に作成できます。 ミニドライバーがこれらのフィルターを登録すると、KSPIN MEDIUM 構造体の**Id**メンバーが一意の値に設定され \_ ます。 ミニドライバーで KSPIN MEDIUM 構造体の**Id**メンバーが一意の値に設定されていない場合 \_ 、graph の自動構築アプリケーションは、必要な隣接するフィルターの読み込みに失敗する可能性があります。 ただし、たとえば、グラフの編集では、手動フィルター (グラフの作成) が引き続き機能する場合があります。

ミニドライバーを DirectShow に登録するには:

- Stream クラスミニドライバーは、 [**StreamClassRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisterfilterwithnokspins)関数を呼び出して、フィルターを DirectShow に登録します。

- AVStream ミニドライバー [**KsRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksregisterfilterwithnokspins)関数を呼び出して、フィルターを DirectShow に登録します。

- または、ミニドライバーが BDA モデルに従い、特定の[**Ksfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)構造にある特定の[**ksfilter \_ 記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造の複数のインスタンスが同じカーネルストリーミングカテゴリに登録されている場合は、 [**KsFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterfactoryupdatecachedata) (または[**BdaFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdafilterfactoryupdatecachedata)) 関数を呼び出して、フィルターを DirectShow に登録します。

\_SRB \_ GET \_ ストリーム \_ 情報 (ストリームクラスミニドライバーの場合) または Kspin DESCRIPTOR EX (avstream ミニドライバーの場合) のいずれかから返される kspin medium 構造体は、 \_ 次の \_ プロパティで返される kspin medium メンバーと一致する必要があり \_ ます。

- Ksk[**プロパティクロスバーの pininfo 構造 \_ 体 \_ \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)の中で、**中程度**の[**メンバー。 \_ \_ **](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo) メディアが一致しない場合、グラフの作成はミニドライバーのフィルターとグラフ内の隣接するフィルターの間で失敗する可能性があります。

- [**Ksk プロパティ \_ チューナー \_ \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)キャップの**videomedium**および**audiomedium**メンバーは、 [**ksk プロパティ \_ チューナー \_ キャップ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-caps)の構造を持ちます。

- Ksk プロパティ[** \_ TVAUDIO \_ caps**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-caps)の[** \_ TVAUDIO \_ Caps \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s)構造体の**inputmedium**および**outputmedium**メンバー。

メディアとメディアの Guid を正しく実装するだけでなく、プロセスが複数のフィルターグラフで動作することを確認するために、他のガイドラインに従う必要があります。 ミニドライバーは、フィルターグラフが ksk 状態の値の** \_ 取得**値である ksk 状態に遷移するまで、ハードウェアリソースをロックすることはできません。 これにより、2つのビルドされた (ただし、実行されていない) フィルターグラフを相互に干渉することなく共存させることができます。

メディアの実装方法など、メディアの詳細については、 [Avstream のシミュレートされたハードウェアサンプルドライバー (AVSHwS)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)に関する説明を参照してください。

> [!NOTE]
> Windows Driver Kit (WDK) サンプルのサンプルコードから新しいミニドライバーを派生させる場合は、デバイスの一意のハードウェアトポロジを反映するために、メディアの新しい GUID 値を生成する必要があります。 そうしないと、別のデバイスに対して定義されているメディアと1つのデバイスのメディアが衝突する可能性があります。
