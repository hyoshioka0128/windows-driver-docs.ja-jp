---
title: DXGI プレゼンテーション パス
description: DXGI プレゼンテーション パス
ms.assetid: 3519172d-261c-4b33-b1e7-c4abf33b15f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f907f9ac6cc3dd085db32a10f347c1bc4891e26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355017"
---
# <a name="dxgi-presentation-path"></a>DXGI プレゼンテーション パス


DXGI はその「なく動作します」プレゼンテーションの方法を使用してアプリケーションを提供します。 たとえば、アプリケーションでは、ウィンドウ表示モードと全画面表示モードの間を遷移する特別な操作を実行する必要はありません。 このプレゼンテーションの方法論は DXGI とユーザー モードは、組み合わせの複数のサンプル アンチ エイリアス (MSAA)、モニターの回転、戻るおよびフロント バッファー サイズと形式、相違点の間でプレゼンテーションを維持するドライバーの動作を表示します。ウィンドウ表示モードと全画面表示します。 DXGI のもう 1 つの利点は、ディスプレイ アダプター スキャン アウト MSAA する機能を制限し、「ステートレス」DDI を提供する DXGI サーフェスを回転できることです。 アダプターのドライバーは、ステートレス DDI, で、DDI 呼び出し間でデータを記録する必要はありません。

プレゼンテーションの基本的なタスクは、表示するためのプライマリ画面にレンダリングされるバック バッファーからデータを移動します。 このタスクは、次のセクションで説明されているさまざまな状況で実行されます。

### <a name="span-idwindowedmodewithdwmonspanspan-idwindowedmodewithdwmonspanwindowed-mode-with-dwm-on"></a><span id="windowed_mode_with_dwm_on"></span><span id="WINDOWED_MODE_WITH_DWM_ON"></span>ウィンドウ表示モードを DWM と

ウィンドウ モードでは、デスクトップ Windows マネージャー (DWM) での大文字と小文字、DXGI は DWM と通信し、DXGI プロデューサーのレンダー ターゲット、DWM のテクスチャにある共有リソースの表示を開きます。 バック バッファー、アプリケーションを作成するだけでなく、この共有リソースが存在します。 DXGI 呼び出してドライバーの[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)背面のいずれかからデータを移動する関数を共有するサーフェスをバッファーします。 この操作は、stretch、色の変換を必要があるし、MSAA を解決します。 ただし、この操作を決してには、サブ元とコピー先の四角形が必要です。 呼び出しで実際には、これらのサブ四角形を表現できない*BltDXGI*します。 このビット ブロック転送 (bitblt) は常に、**存在**フラグを設定、**フラグ**のメンバー、 [ **DXGI\_DDI\_ARG\_BLT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_blt)構造体、 *pBltData*パラメーターを指します。 設定、**存在**フラグは、ドライバーが、操作をアトミックに実行する必要があることを示します。 ドライバーでは、DWM が合成の共有リソースを読み取る間に分裂の可能性を最小限に抑えるためには、アトミックに bitblt 操作を実行します。

### <a name="span-idwindowedmodewithdwmoffspanspan-idwindowedmodewithdwmoffspanwindowed-mode-with-dwm-off"></a><span id="windowed_mode_with_dwm_off"></span><span id="WINDOWED_MODE_WITH_DWM_OFF"></span>オフ DWM とウィンドウ表示モード

DWM オフの場合とウィンドウ表示モード、DXGI 呼び出してドライバーの[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数と、 **Blt**フラグを設定、**フラグ**メンバー、 [ **DXGI\_DDI\_ARG\_存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present)構造体、 *pPresentData*パラメーターが指す宛先。 この*PresentDXGI*呼び出し、DXGI 指定可能な内のアプリケーションで作成されたバック バッファー、 **hSurfaceToPresent**と**SrcSubResourceIndex** DXGIのメンバー\_DDI\_ARG\_存在します。 共有画面を追加することはありません。

### <a name="span-idfullscreenmodespanspan-idfullscreenmodespanfull-screen-mode"></a><span id="full_screen_mode"></span><span id="FULL_SCREEN_MODE"></span>全画面表示モード

全画面表示の場合は、DWM とウィンドウ表示モードのオンまたはオフするより複雑です。

DXGI が全画面表示モードへの切り替えを行うと、帯域幅を減らすし、垂直同期の同期を取得するために、反転操作を悪用しようとします。 次の条件には、フリップ操作の使用を回避できます。

-   アプリケーションは、プライマリの画面と一致するように、バック バッファーを再割り当てられませんでした。

-   ドライバーは、これはスキャン アウトされていないバック バッファー (たとえば、バック バッファーは回転かため MSAA) を指定します。

-   アプリケーションでは、Direct3D ランタイムが、バック バッファーの内容の破棄と (合計) チェーン内の要求された 1 つだけバッファーを受け付けられないことを指定します。 (ここでは、DXGI はバック サーフェイスおよび面のプライマリを割り当てます DXGI がドライバーのはどのように使用するただし、 *PresentDXGI*関数と、 **Blt**フラグを設定します。)。

フリップ操作と、ドライバーへの呼び出しを防ぐ、上記の条件のいずれかが発生したときに[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数と、 **Blt**フラグが設定されても不適切 (バック バッファーでは、フロント バッファーを正確に一致しない) ため、DXGI 割り当てます、*プロキシ画面*します。 このプロキシ サーフェスでは、フロント バッファーと一致します。 そのため、プロキシの画面とフロント バッファー間の反転可能になります。 DXGI がドライバーを使用して、プロキシの画面が存在する場合は、 [ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数と、**存在**フラグは、プロキシの画面に、アプリケーションのバック バッファーをコピーする (0) をクリアします。 この*BltDXGI*呼び出し、DXGI は変換、拡大、および解決を要求可能性があります。 DXGI を呼び出してドライバーの*PresentDXGI*関数と、**反転**フラグを設定、**フラグ**のメンバー、 [ **DXGI\_DDI\_ARG\_存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present)構造をスキャンするプロキシ サーフェスに移動します。

ドライバーでは、ユーザー モードのディスプレイ ドライバーをドライバーがスキャンからオプトアウトできますが、通知をスキャン アウト サーフェスの省略可能で、省略できないクラスのリソースの作成の呼び出しが表示されます。 省略可能なスキャン アウト サーフェスは、DXGI によって指定された\_DDI\_プライマリ\_オプションのフラグ。 非省略可能なスキャン アウト サーフェス、DXGI がない\_DDI\_プライマリ\_省略可能なフラグを設定します。 これらの種類のリソースの作成の呼び出しの詳細については、次を参照してください。[リソースの作成時に DXGI の情報を渡す](passing-dxgi-information-at-resource-creation-time.md)します。

DXGI 設定、DXGI\_DDI\_プライマリ\_戻るすべてを作成する省略可能なフラグ バッファー サーフェス (つまり、省略可能なサーフェス) のフロント バッファーまたはプロキシ サーフェイス (つまり、省略できない画面) フラグを設定していないとします。

場合 DXGI\_DDI\_プライマリ\_バック バッファー (省略可能) に設定されて、ドライバーは、DXGI を設定できる\_DDI\_プライマリ\_ドライバー\_フラグ\_ありません\_SCANOUT フラグ。 このフラグを設定する方法についての詳細については、次を参照してください。[リソースの作成時に DXGI の情報を渡す](passing-dxgi-information-at-resource-creation-time.md)します。 ドライバーは、DXGI を設定する場合\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_SCANOUT 省略可能なバッファーを影響を与えません以外を呼び出してドライバーの DXGI させる[**PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数と、 **Blt**フラグの設定の代わりに、**反転**フラグを設定します。

場合 DXGI\_DDI\_プライマリ\_フロント バッファーまたはプロキシの画面のオプションが設定されていない、ドライバーが無効にできますスキャン アウト DXGI のエラー コードでリソースの作成の呼び出しが失敗したことで\_DDI\_ERR\_サポートされていないと設定する DXGI\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_SCANOUT します。

**注**   DXGI を設定せず、作成の呼び出しを失敗\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_SCANOUT は実際に障害の場合、予約されていますメモリ不足など。

 

DXGI は、MSAA または回転のバック バッファーの全画面プレゼンテーション チェーンを作成しようとしたときに、このオプトアウトの方法論を悪用します。 ドライバーはスキャン アウトされていないいずれかまたは両方の型場合、ドライバーがオプトアウトします。DXGI、しようと、ドライバーは、リソースの作成を受け入れるまで、回転されていない画面、非 MSAA サーフェス、またはその両方を作成します。 そのため、DXGI はフォールバック段階的にオプションで非までフロント バッファーのフォーマット、サンプルの数、回転、およびサイズ、画面が正確に一致します。

場合は、省略できない画面オプトアウトするドライバー、DXGI 必要があるプライマリのサーフェイスにバック バッファーからのビットを移動する方法。 そのため、スキャン アウト MSAA と回転をオプトアウトするドライバー場合、ドライバー opts で解決、回転、またはその両方を DXGI 呼び出すドライバーの[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数。 DXGI はプロキシ画面と呼び出しを作成、ドライバーが opts するとき**BltDXGI**バック バッファーからそのプロキシの画面にデータを移動します。 ドライバーには、オプトアウトこのプロキシのサーフェイスのプロキシは、フロント バッファーを正確に一致するために理由はありません。

次の特殊な状況は、アプリケーションで再作成されない、サーフェスにするか、全画面表示モードからの移行が完了した後ときに発生します。

-   場合は、アプリケーションは、サーフェスが全画面表示モードになったときに再作成していない、DXGI を決定しますバック バッファーには、前面のバッファーは一致しない場合でも、形式、サイズ、回転、およびサンプルの数を実際に一致しています。 この決定の理由は、オペレーティング システムが、特定のモニタをスキャンするためにタグ付けするこれらのバッファーを作成するときにバック バッファーが必要であります。 ウィンドウのバック バッファーことはできませんが明確にまだ割り当てられて、特定のモニタ モニターは全画面表示が入力したときに動的に選択されているためです。 そのため、DXGI はスキャン アウト (フリップ操作) でのドライバーにこれらのバック バッファーを送信する必要があります。 この種類のアプリケーションでは、プロキシ画面を作成する DXGI 通常強制します。

-   DXGI がドライバーを呼び出すことができる場合、アプリケーションは、バック バッファーがウィンドウ表示モードに戻ったときに再作成していない、 [ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)または[ **PresentDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (で**Blt**設定) の反転操作を既に作成されている画面で、bitblt 関数を実行します。 このような状況では、問題をすることはできませんが、完全を期すのためここで説明されています。 アプリケーションがウィンドウ表示モードに移行するときに、DXGI がそのプロキシ サーフェスを常に破棄することに注意してください。

また、ことアプリケーション サイズを変更できる、バック バッファーに動的に、アプリケーションが全画面表示モードでは注意してください。 この操作では、再度発生する前の状況で説明されているロジックにより、します。 そのため、プロキシ画面を作成および破棄される可能性がありますされ、したりできない可能性があります必要な時間の経過と共に、アプリケーションは全画面表示モードのままでもオプト アウト。 アプリケーションに転送できます出力別のモニターに動的に全画面表示モードを離れることがなく。 そのため、別のモニターのアプリケーションのバック バッファーのタグ付けされたために、アプリケーションは、bitblt モードに戻すスイッチが発生します。

最後に、MSAA スキャン アウト、ドライバーは無効にしない場合は、MSAA バック バッファーに関して発生する場合の注意する必要があります。このような状況では、ドライバーは、MSAA のスキャン アウトで opts します。 そのため、MSAA バック バッファーとを通じて MSAA フロント バッファー DXGI インターチェンジは、操作を反転し、アナログ デジタル コンバーター (DAC) と同等で解決操作を実行します。 このような状況で、アプリケーションには、ドライバーの呼び出しに切り替える DXGI を強制する全画面表示モードでは動的にバック バッファーもサイズを変更できます[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数。 フロント バッファー、バック バッファーの MSAA 特性も一致しているために、DXGI にドライバーが解決する以外、色変換する可能性があります、ストレッチ bitblt を実行することを指定します。 ドライバーする必要がありますし、レプリケートを解決することがなく、ドライバーがスキャン アウト MSAA を選択した場合に必要なフロント バッファーにマルチ サンプル。

 

 





