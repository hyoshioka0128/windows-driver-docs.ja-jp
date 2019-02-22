---
title: スライサーの設定
description: XML 構成ファイルには、さまざまな Windows の 3D 印刷ダイアログ ボックスに公開されている印刷機能を制御する特定の 3D プリンター デバイスに合わせて調整する必要がある設定が含まれています。
ms.assetid: 9203AABB-48D9-47A6-A2B1-7A878BF82FD1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ed24f5c8807b10ef5a838feb52148676af22b3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559165"
---
# <a name="slicer-settings"></a>スライサーの設定


XML 構成ファイルには、さまざまな Windows の 3D 印刷ダイアログ ボックスに公開されている印刷機能を制御する特定の 3D プリンター デバイスに合わせて調整する必要がある設定が含まれています。 これらの設定では、Microsoft 3D のスライサー (MS3DPrinterRenderFilter.DLL と依存関係) の実行パラメーターも制御します。  

## <a name="slicer-settings"></a>スライサーの設定


<table>

<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>

<thead>
<tr class="header">
<th>設定 (XML パス)</th>
<th>[Change]</th>
<th>説明</th>
</tr>
</thead>

<tbody>

<tr>
<td><p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaWidth</p>
<p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaDepth</p>
<p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaHeight</p></td>
<td><p>〇</p></td>
<td><p>幅 (最大 x)、深度 (最大 y)、高さ (z が最大) で定義されているミクロンでボリュームを印刷します。</p>
<p>ボリュームには、プリンターが宣言されているボリュームを使用できますが、ドライバーの発行、認定フェーズでのテストの 1 つとして、物理デバイスの機能を表す必要があります。</p></td>
</tr>


<tr>
<td><p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaOffsetX</p>
<p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaOffsetX</p></td>
<td><p>省略可能</p></td>
<td><p>関連する印刷量の X と Y のオフセット (0, 0)。 これにより、3 D プリンターのサポート、(0, 0)、ベッド (標準のデルタ プリンター) またはプリンターの中央には、(0, 0) 印刷ベッドの左上隅の前面にないです。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3ds:extruders\  </p></td>
<td><p>省略可能</p></td>
<td><p>プリンターで extruders の数。 この設定を制御数の後続の psk3d:Material&lt;マット&gt;セクションでは、XML では、印刷機能として、印刷ダイアログ ボックスに送信されます。 指定しない場合、ドライバーは 1 つ extruder プリンターと想定されます。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk:DisplayName</p></td>
<td><p>〇</p></td>
<td><p>素材の表示名。 これにより、ユーザーの割り当ての 3D 印刷 ダイアログ ボックスに表示される任意の文字列がでことができます。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk:MaterialColor</p></td>
<td><p>〇</p></td>
<td><p>3D 印刷 ダイアログ ボックスでは、素材のレンダリングの RGB または RGBA 色です。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk:MaterialType</p></td>
<td><p>予約済み</p></td>
<td><p>3D 印刷用の印刷スキーマのキーワードで定義されている素材の種類 (たとえば、 &quot;psk3d:PLA&quot;)。 名と色で指定された汎用の資料を優先してこの設定は非推奨です。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk3dx:platformtemperature</p></td>
<td><p>〇</p></td>
<td><p>印刷のベッドを印刷時に過熱する必要があります温度 (摂氏)。 値の 0 の場合は、ベッドは白熱いない必要があります。</p>
<p>この値を使用して後で参照できます、 <em>$platformtemperature$</em>前のコマンドでテンプレート。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk3dx:filamentdiameter</p></td>
<td><p>〇</p></td>
<td><p>3D のプリンターでの・ フィラメント ・ ミクロン直径が読み込まれます。 たとえば、1750 では、標準の 1.75 mm ・ フィラメント ・です。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk3dx:filamentcalibrationoverride</p></td>
<td><p>省略可能</p></td>
<td><p>・ フィラメント ・のフローを調整する係数。 (に基づいて filamentdiameter) 3-d の速度を調整する着信・ フィラメント ・ セクションの比率として適用されます。 この要素が 1.0 よりも大きい場合は、小さいプラスチックの 3-d されます。 これはチューニング パラメーターであり、1.0 ほぼ常にする必要があります。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk3dx:extrudertemperature</p></td>
<td><p>〇</p></td>
<td><p>摂氏で温度押し出しときに熱 extruder ホット/終了する必要があります。 この値から参照できる、 <em>$extrudertemperature$</em>前のコマンドでテンプレート。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;マテリアル&gt;\ </p>
<p>psk3dx:autocenter</p></td>
<td><p>省略可能</p></td>
<td><p>示すブール値 (0 または 1) (XY 平面) で印刷のベッドにモデルを中央揃えにするかどうか。 モデルも自動の中心は印刷量に収まらない場合です。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d:Material&lt;マテリアル&gt;\  </p>
<p>psk3dx:SetupCommands\ </p>
<p>psk3dx:command</p></td>
<td><p>〇</p></td>
<td><p>セットアップの材料として使用するコマンドの一覧。 これは、準備、nozzle の事前暖房を制御するための前のコマンドの中に実行される通常の G コードです。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d:Material&lt;マテリアル&gt;\  </p>
<p>psk3dx:SelectCommands\ </p>
<p>psk3dx:command</p></td>
<td><p>〇</p></td>
<td><p>素材が印刷中に使用する必要がある場合に発行するコマンドの一覧。 これは、に対して実行される通常の G コードです。T0/T1 extruder 選択した場合、nozzle のシーケンスでのワイプは、ファンに/オフ/段階的なを有効にする、材料、温度、および具合を取り消します。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d:Material&lt;マテリアル&gt;\  </p>
<p>psk3dx:DeselectCommands\ </p>
<p>psk3dx:command</p></td>
<td><p>〇</p></td>
<td><p>印刷時に、リソースが解放されるときに発行するためのコマンドの一覧。 これは通常 G-コードの実行: 材料を取り消し、nozzle が駐車温度の削減および具合です。</p></td>
</tr>

<tr>
<td><p>psk3dx:customStatus</p></td>
<td><p>省略可能</p></td>
<td><p>通常、スライスのフェーズの初期の印刷ジョブの状態を表す文字列。 ジョブの状態に設定がない場合、&quot;印刷&quot;します。 通常この値に設定する必要があります&quot;Slicing&quot;スライスが行われるタイミング レンダー フィルターでなど、Microsoft のスライサーを使用する場合。</p></td>
</tr>

<tr>
<td><p>psk3dx:userprompt</p></td>
<td><p>〇</p></td>
<td><p>メッセージが表示されます、印刷する前に、ユーザー プロンプトを開始します。 このプロンプトは、extruder の印刷を手動で削除を必要とするデバイス上の既存の印刷にクラッシュを防ぐために使用されます。</p>
<p>先頭または印刷の末尾には、デバイス自体では、プロンプトを表示できるデバイスの場合は、この設定は必要ありません。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:debug\ </p>
<p>psk3dx:log</p></td>
<td><p>省略可能</p></td>
<td><p>存在する場合、この設定は、ので、開発者は、G コードおよびファームウェアの応答を検査するファイルにログ記録するドライバー デバッグを有効します。</p>
<p>この設定も可能にグローバルに HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print のレジストリ キーを使用して</p>
<p>StandardGCodeDebugLog=&quot;c:\Path\To\LogFile&quot;</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx: comport</p></td>
<td><p>省略可能</p></td>
<td><p>シリアル ポート名への URI。 存在する場合、この設定は、COM ポートのドライバーの自動解決をオーバーライド (プリンター キュー -&gt;プリンター ポート名 -&gt; Enum\3DPrinter\Device -&gt; Enum\USB\Serial デバイス)。 これにより、最後のハードウェア Id がないデバイスに一時的に印刷できます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:baudrate</p></td>
<td><p>省略可能</p></td>
<td><p>接続されたデバイスのシリアル接続のボー レート。 一般的な値は、115200 または 250000 です。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:mode</p></td>
<td><p>予約済み</p></td>
<td><p>この設定の制御、リセットの動作 (DTR の設定) を接続します。 デバイスが接続できない場合は、1 または 3 の値を使用します。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\  </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:protocol</p></td>
<td><p>予約済み</p></td>
<td><p>この設定は実験的な高度であり、ファームウェアを使用して、通信プロトコルを制御します。 指定しない場合、ドライバーによって RepRap/カジキのチェックサムを含む ASCII G コードが既定値です。 2 に設定すると、ドライバーは G のバイナリ コードを送信できます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:timeout</p></td>
<td><p>予約済み</p></td>
<td><p>プリンターの応答をミリ秒でタイムアウトします。 タイムアウトなしの値を 0 (既定値) を使用します。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:initcommands\ </p>
<p>psk3dx:command</p></td>
<td><p>〇</p></td>
<td><p>スライスする前に送信されたコマンドのシーケンス。 これらのコマンドは、スライサーを並列で実行されます。 これは、通常、調整、自動レベルやほぼの最終的な温度にプリンターを熱 G コード コマンドのシーケンスです。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:precommands\ </p>
<p>psk3dx:command</p></td>
<td><p>〇</p></td>
<td><p>一般に、各ジョブの開始時に回帰と最終的な温度 extruder を暖房、extruder の準備など、3 D プリンターを初期化するために送信する G コード コマンドのセット。 各デバイスには、別の必要な事前コマンドがあります。 G コードの各行は、子に反映する&lt;コマンド&gt;要素。 参照されている設定によって置換される変数を '$' 文字で区切られた名前として宣言できます&lt;コマンド&gt;M104 <em>S$ extrudertemperature$</em>&lt;/command&gt;. 組み込み変数は次のセクションを参照してください。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:postcommands\ </p>
<p>psk3dx:command</p></td>
<td><p>〇</p></td>
<td><p>安全な状態では、3 D プリンターに一般に、各ジョブの最後に送信する G コード コマンドのセットなど、extruder ダウン冷却先 extruder ホット/末尾から一部を移行、&#39;、ベッドから削除するの簡単です。 各デバイスには、別の必要な後コマンドがあります。</p>
<p>このシーケンスは、ジョブがキャンセルされたときにも実行されます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:failsafepostcommands\ </p>
<p>psk3dx:command</p></td>
<td><p>省略可能</p></td>
<td><p>スライサーのエラーが発生した場合など、安全なメカニズムが失敗するように送信される G コード コマンドのセット。 ドライバーの実行は、不足している場合、 &quot;M110 N0&quot;続けて&quot;M104 S0&quot;します。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:layerthickness</p></td>
<td><p>〇</p></td>
<td><p>ミクロンのレイヤーの太さ (z 高さ)。 この値は、配置エラーを最小限に抑えるマシンの物理的な解像度に基づいて定義する必要があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:maxlayerthickness</p></td>
<td><p>予約済み</p></td>
<td><p>ミクロンで最大のレイヤーの太さです。</p>
<p>この設定は、予約されており、今後非推奨可能性があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:minlayerthickness</p></td>
<td><p>予約済み</p></td>
<td><p>ミクロンで最小のレイヤーの太さです。</p>
<p>この設定は、予約されており、今後非推奨可能性があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:pathwidth</p></td>
<td><p>〇</p></td>
<td><p>ミクロン押し出された toolpath の (XY 平面) の幅。 近いと若干より大きい値 nozzle 直径は最良の結果を生成する傾向があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:shells</p></td>
<td><p>省略可能</p></td>
<td><p>Infill 開始する前に、埋め込みシェルの整数値。 値 1 は 1 つの境界のみを行い、値 0 の場合、唯一 infill (非常に大まかな表面の終了日)。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:shelloffset</p></td>
<td><p>省略可能</p></td>
<td><p>ミクロンで外部のシェルのオフセット。 部分 (gears など) の間で非常に密接な調整を備えているモデルで結果をチューニングするのにには、この値を使用します。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:topsurfacelayers</p></td>
<td><p>省略可能</p></td>
<td><p>印刷の上部のサーフェスに堅固入力層の整数値。 値 0 では、スパース infill が上から表示します。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:bottomsurfacelayers</p></td>
<td><p>省略可能</p></td>
<td><p>印刷の下の画面に堅固入力層の整数値。 値 0 では、スパース infill を下部にある表示にします。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:fill</p></td>
<td><p>予約済み</p></td>
<td><p>0.0 ~ 1.0 までの範囲、スパース infill 分数を指定します。 0.1 (10%)適切な既定値です。 値が 0.0 の印刷されているシェルのみが発生し、値が 1.0 のでは、solid infill パターンはスパース infill の代わりに使用します。</p>
<p>この設定は、予約されており、今後非推奨可能性があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:fillangle</p></td>
<td><p>省略可能</p></td>
<td><p>塗りつぶしのパターンの最初の角度は、面に沿った XY (水平)、x 軸から反時計回りに度数で測定されます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:filloverlap</p></td>
<td><p>予約済み</p></td>
<td><p>(0 と 1 の包括的なパスの幅) の間の重複を infill します。</p>
<p>この設定は、予約されており、今後非推奨可能性があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:speed</p></td>
<td><p>〇</p></td>
<td><p>ミクロン/秒で、動きの印刷の既定の速度。 これは、X と Y 軸の速度の 2 つのノルムです。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:speedouter</p></td>
<td><p>〇</p></td>
<td><p>外側の境界の速度 (最初は、シェル) ミクロン/秒します。 これは、印刷に優れた表面の仕上げを作成する標準の速度よりも低い設定することができます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:speedfirst</p></td>
<td><p>〇</p></td>
<td><p>最初のレイヤーの速度 (置き換え<strong>speedouter</strong>) ミクロン/秒します。 これは、標準の速度向上の印刷ベッド adhesion を作成するよりも低い設定することができます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:speedtravel</p></td>
<td><p>〇</p></td>
<td><p>浮き出し以外の速度は、ミクロン/秒に移動します。 これは、標準の速度を糸を最小限に抑え、extruder が制限要因の場合、印刷速度よりも高く設定することができます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:speedretract</p></td>
<td><p>〇</p></td>
<td><p>・ フィラメント ・取り消しおよびミクロンでプッシュ バックの速度/秒します。 その他の速度の設定とは異なり、X と Y 軸ではなく、入力の・ フィラメント ・単位は。 この速度は 20 (、・ フィラメント ・) に応じて上記速度よりも小さいためです。 ただし、同等の速度より高いあるためにありますプラスチックが取り消し中に面を浮き出し表示に強制されません。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:retraction</p></td>
<td><p>〇</p></td>
<td><p>取り消す・ フィラメント ・の長さは、もう一度ミクロンの入力・ フィラメント ・で測定されます。 これは取り消しおよび戻す対称であり、組み合わせると、出張した場合、nozzle のにじみの削減は設計されています。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:supportorientationoptimization</p></td>
<td><p>予約済み</p></td>
<td><p>ブール値 (0 または 1) に自動的に必要なサポートを最小限に抑えるか、モデルの方向を変更するかどうかを示します。</p>
<p>この設定は、予約されており、今後非推奨可能性があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:supportoverhangangle</p></td>
<td><p>省略可能</p></td>
<td><p>最大値では、角度 (度単位)、モデルのファセットの最大水平面から測定のサポートを必要とするオーバー ハングできます。 小さい角度は、以下のサポート構造を作成します。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:supportzgap</p></td>
<td><p>〇</p></td>
<td><p>一部のサポートとミクロン Z 間隔。 この設定は、サポートを簡単に削除をサポートする adhesion を減らすことができます。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:supportxygap</p></td>
<td><p>〇</p></td>
<td><p>ミクロン サポートと XY 平面にパーツ間の間隔。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:supportfill</p></td>
<td><p>省略可能</p></td>
<td><p>(0 と 1、包括的) の間のサポートのスパース infill 分数。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:raftlayers</p></td>
<td><p>省略可能</p></td>
<td><p>Solid ラフト レイヤーの数。 数値として 2 は、一般に十分です。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:raftlayerthickness</p></td>
<td><p>〇</p></td>
<td><p>ミクロン ラフトのレイヤーの太さ (Z 高さ)。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:raftpathwidth</p></td>
<td><p>〇</p></td>
<td><p>ミクロン ラフトのパスの幅。 これは、一般に、印刷ベッド サーフェスの変動に対応するより大きい値です。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:raftfill</p></td>
<td><p>省略可能</p></td>
<td><p>(0 と 1、包括的) の間のサポートのスパース infill 分数。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:raftoffset</p></td>
<td><p>省略可能</p></td>
<td><p>ミクロン ラフトのサイズ。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:raftzgap</p></td>
<td><p>〇</p></td>
<td><p>ミクロン、ラフトとオブジェクトの間で Z 間隔。 高い値を指定すると、ラフトは簡単に削除するが不均一の画面を生成する可能性があります。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:raftspeedfirst</p></td>
<td><p>〇</p></td>
<td><p>ラフトの速度第一層でミクロン/秒。 類似または下にあります<strong>speedfirst</strong>ベッド adhesion を向上させる。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:coolingtime</p></td>
<td><p>省略可能</p></td>
<td><p>レイヤーの時間 (秒) を冷却する最小値。 この秒数よりもさらに印刷されるよう、レイヤーの速度が低下します。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:mincoolingspeed</p></td>
<td><p>省略可能</p></td>
<td><p>ミクロン/秒のレイヤーの速度を冷却する最小値。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx:{quality}\ </p>
<p>psk3dx:bridgingspeed</p></td>
<td><p>〇</p></td>
<td><p>ミクロン ブリッジでの 3-d の速度です。 この値は、マシン冷却装置の特性と・ フィラメント ・型などの要因によって異なります、通常、印刷速度が通常より低速です。</p></td>
</tr>

</tbody>
</table>


**注**印刷ノードの設定 (psk3dx:MS3DPrinter\\psk3dx:print\\psk3dx: {0} 品質}\)、{品質} の要素名は対応する psk3d:Quality 印刷スキーマの 3D キーワードのいずれかで置き換えられます印刷ジョブと共に PrintTicket の送信の設定です。 これにより、独自のスライサーの設定セットを定義するには、各品質レベル。 スライサー、PrintTicket を省略すると、使用、\[品質\]既定の属性でマークされた設定 ="true"にすると、まったく常に、1 つの品質レベルはこの属性を定義する可能性があります。

<table>

<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>

<thead>
<tr class="header">
<th>設定名</th>
<th>説明</th>
</tr>
</thead>
<tbody>

<tr>
<td><p>$extrudertemperature $</p>
<p>extruder2temperature $ $</p></td>
<td><p>最初のそれぞれで指定したとおり、2 つ目の extruder の温度&lt;psk3dx:extrudertemperature&gt;資料」の XML にします。 これらの変数は非推奨とされている $MaterialSetup$ によって置き換えられるとします。</p></td>
</tr>

<tr>
<td><p>$platformtemperature $</p></td>
<td><p>指定された過熱ベッドの温度、 &lt;psk3dx:platformtemperature&gt;の一覧で、最後のマテリアル内のエントリ。</p></td>
</tr>

<tr>
<td><p>$MaterialSetup<n>$</p></td>
<td><p>素材のセットアップ セクション&lt;psk3dx:SetupCommands&gt;資料にします。 たとえば MaterialSetup3 $$ は、一覧で、3 番目の extruder 通常サード マテリアルを表します。</p></td>
</tr>

<tr>
<td><p>$rampup $</p></td>
<td><p>これは、変数を 0..255 は、および Z 軸を拡大または縮小し、によって制御されます、 &lt;psk3dx:rampuptarget&gt;スライサーの品質設定でします。</p>
<p>たとえばコマンド&quot;M106 S$ rampup$&quot;段階的には Z 軸が増加するにつれて、ファンをオンにします。 場合、 &lt;psk3dx:rampuptarget&gt;設定されている 500 ミクロン、変数の値とする最初のレイヤーでは、0 から 255 レイヤーが 500 ミクロン以上。</p>
<p>この変数が過熱印刷ベッドで印刷 adhesion の向上をサポートするものですが、任意のコマンドで使用できます。</p></td>
</tr>

<tr>
<td><p>;?ack=&lt;pattern&gt;</p></td>
<td><p>この設定が既定値から、コマンド確認パターン (プリンターの応答) を変更するドライバーに指示&#39;ok&#39;例については、一時的なものに&quot;; でしょうか。ack をファイルに書き込みを =&quot;プリンターの内部ストレージに書き込む準備が確認を待機するドライバーに話したことでしょう。</p></td>
</tr>

<tr>
<td><p>;?err=&lt;pattern&gt;</p></td>
<td><p>この設定を既定値をさらに応答をプリンターの追加のエラー パターンを検索するドライバーに指示&#39;エラー&#39;します。 たとえば"; でしょうか。err = オープンに失敗しました"(この例は、ハードウェアの SD カードの内部記憶域が初期化されていない場合は、この応答を返すまたは完全) では、このような応答が受信したかどうか、ドライバーがエラーに話したことでしょう。</p></td>
</tr>

<tr>
<td><p>;?wait=&lt;pattern&gt;</p></td>
<td><p>この設定をパターンを無視するドライバーに指示キープ アライブ信号で通常使用して、既定値は '; でしょうか。待機待機を =' です。</p></td>
</tr>

</tbody>
</table>




