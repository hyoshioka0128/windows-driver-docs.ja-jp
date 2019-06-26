---
title: メディアの GUID
description: メディアの GUID
ms.assetid: 4209952c-0ba5-4359-b612-91529a0a46f1
keywords:
- ビデオ キャプチャ WDK AVStream、メディア
- ビデオの WDK AVStream、メディアのキャプチャ
- メディアの WDK ビデオのキャプチャ
- 暗証番号 (pin) の接続の WDK ビデオ キャプチャ
- Guid の WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e0f609f9cfe0a8ce45d6c6bcadda5413e35c023
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386633"
---
# <a name="medium-guids"></a>メディアの GUID


ミニドライバーは、複数のデバイスをサポートできる必要があります。 さらに、フィルターをストリーミングする別のカーネルには、テレビやラジオ チューナー、テレビのオーディオ、クロスバー、およびビデオ キャプチャ コンポーネントが区切られた、ため、メソッドが正しくでこれらのコンポーネント間の位相的なハードウェアの接続を記述するために必要なデバイスも複数のデバイスで同様です。 たとえば、2 つのビルドが実行されていないフィルター グラフを FM ラジオをサポートしてと TV キャプチャは、共存できる必要があります。 ミニドライバーは、これらのシナリオに対応するのにメディアを使用します。 フィルターのグラフなど、アプリケーションの構築も、*グラフの編集*フィルターのグラフの構築時にメディアを使用して、別のデバイスのフィルターに 1 つのデバイスのフィルターが正常に接続していることを確認します。 たとえば、デバイスの 1 つのチューナーのフィルターする必要がありますを別のデバイスのクロスバー フィルターは接続できません。

ミニドライバーでメディアの説明、 [ **KSPIN\_MEDIUM** ](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85)) GUID データ型のメンバーで構成される構造 (**設定**) 後に 2 つの ULONG メンバー (**Id**と**フラグ**)。

-   **設定**位相的なハードウェアの接続を表す GUID をメンバーに割り当てる必要があります。

-   ミニドライバーを設定する必要があります、 **Id**デバイス インスタンスの一意の値のメンバー。

-   **フラグ**メンバーは、システムの使用に予約されているし、0 に設定する必要があります。

システムでは、存在する複数のデバイスでフィルター グラフの構築が適切なことを確認する、**設定**、KSPIN のメンバー\_中規模の構造はデバイスのインスタンスごとに同じです。 ただし、ミニドライバーは、一意の値を割り当てる必要があります、 **Id** 、KSPIN のメンバー\_デバイス インスタンスごとの中規模の構造体。 設定に失敗した、 **Id**一意の値にメンバーが複数のデバイスがシステムに存在する場合に問題になります。 システムでは、2 つのデバイスがインストールされている場合、ミニドライバーを設定する必要があります、 **Id**デバイス インスタンスごとに別の値にメンバー。 なお、 **Id**同じ 1 つのチューナーと置き換えてなどのハードウェア上に存在するデバイスのフィルターのメンバーは同じである必要があります。 いることを確認する方法の 1 つ、 **Id**メンバーは、デバイスのインスタンス間で異なれば、ミニドライバーにグローバル カウンタがあり、設定する前に、デバイス プラグ アンド プレイの開始時にそのカウンターをインクリメントする**Id**の値にします。

ストリーム、ミニドライバーに続くインターフェイス (AVStream または Stream クラス)、カーネルによって、ミニドライバーの値を指定する必要があります、 **Id**メンバーが異なります。

-   Stream クラス ミニドライバーが処理するときに、値を指定[ **SRB\_取得\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)します。

-   AVStream ミニドライバーの値を指定する、 [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 KSPIN で値を指定する AVStream ミニドライバーの独立した 2 つの方法があります\_記述子\_構造 EX:

    1.  グローバルで静的な記述子を提供**Id**カウンターと呼び出し[  **\_KsEdit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-_ksedit)中に*追加*または*開始*を変更するハンドラーのディスパッチ、 **Id**メンバーを一意の値。
    2.  呼び出す[ **KsCreateFilterFactory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatefilterfactory)中に/ピン留めするフィルター記述子を動的に構築する*追加*または*開始*ハンドラーにディスパッチします。

ミニドライバーは、アプリケーションが実際に作成しないため、テレビやラジオ チューナー、テレビのオーディオ クロスバー フィルターとフィルターのグラフが自動的に作成できるようにする Microsoft DirectShow に自身を登録、特殊な関数を呼び出す必要がありますもカーネル ストリーミングの入力と出力の pin。 設定する必要がありますが、ミニドライバーは、これらのフィルターを登録する場合、 **Id** 、KSPIN のメンバー\_中規模の構造を一意の値。 ミニドライバーが設定されていない場合、 **Id** 、KSPIN のメンバー\_中は、自動グラフのアプリケーションを構築が必要な隣接するフィルターの読み込みに失敗することができますし、一意の値構造体します。 ただし、手動フィルター-グラフの作成、グラフの編集で、動作もあります。

DirectShow: ミニドライバーに登録するには

-   Stream クラス ミニドライバーの呼び出し、 [ **StreamClassRegisterFilterWithNoKSPins** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisterfilterwithnokspins) DirectShow にフィルターを登録する関数。

-   AVStream ミニドライバーの呼び出し、 [ **KsRegisterFilterWithNoKSPins** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksregisterfilterwithnokspins) DirectShow にフィルターを登録する関数。

-   または、ミニドライバー BDA モデル、および特定の複数のインスタンスに従う場合[ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)特定構造[ **KSDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice)構造がカテゴリをストリーミングする同じカーネルで登録すると、呼び出し、 [ **KsFilterFactoryUpdateCacheData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilterfactoryupdatecachedata) (または[**BdaFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdafilterfactoryupdatecachedata)) には、DirectShow フィルターを登録する関数。

KSPIN\_SRB のいずれかから中規模の構造が返される\_取得\_ストリーム\_(の Stream クラス ミニドライバー) の情報または KSPIN\_記述子\_(AVStream ミニドライバーの場合) の例に一致する必要がありますKSPIN\_中程度のメンバーは、次のプロパティで返されます。

-   **Medium**のメンバー、 [ **KSPROPERTY\_クロスバー\_PININFO\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)の構造[ **KSPROPERTY\_クロスバー\_PININFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo)します。 メディアが一致しない場合、グラフの構築は、ミニドライバーのフィルターと、グラフの横にあるフィルター間フェールオーバーできます。

-   **VideoMedium**と**AudioMedium**のメンバー、 [ **KSPROPERTY\_チューナー\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)の構造[ **KSPROPERTY\_チューナー\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-caps)します。

-   **InputMedium**と**OutputMedium**のメンバー、 [ **KSPROPERTY\_TVAUDIO\_CAP\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s)の構造[ **KSPROPERTY\_TVAUDIO\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-caps)します。

メディアと中程度の Guid を正しく実装するだけでなく、プロセスは、複数のグラフをフィルターを使用できることを確認するには、その他のガイドラインに従うために必要なは。 ミニドライバーは、フィルターのグラフに遷移するまで、ハードウェア リソースをロックする必要があります、 **KSSTATE\_ACQUIRE** KSSTATE の値。 これにより、構築された、2 つが、互いに干渉することがなく共存できるグラフのフィルターが実行されていません。

その実装方法などのメディアの詳細については、次を参照してください。、 [AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)します。

**注**  :Windows Driver Kit でサンプル コードから新しいミニドライバーを派生している場合は、デバイスの一意のハードウェア トポロジを反映するようにメディアの新しい GUID 値を生成する必要があります。 そのために発生する可能性が 1 つのデバイスが競合する別のデバイスに対して定義されているメディアのメディア。

 

 

 




