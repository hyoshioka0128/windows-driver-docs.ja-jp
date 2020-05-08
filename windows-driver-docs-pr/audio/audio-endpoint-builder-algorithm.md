---
title: Audio Endpoint Builder のアルゴリズム
description: Audio Endpoint Builder のアルゴリズム
ms.assetid: 2338bca7-5743-42c3-9baf-ac4a54cf0393
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abc4e19b3d04a3e7f31ee31c036d6d8042703611
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925507"
---
# <a name="audio-endpoint-builder-algorithm"></a>Audio Endpoint Builder のアルゴリズム


Windows Vista 以降のバージョンの Windows では、AudioEndpointBuilder は、システム内のオーディオエンドポイントを列挙、初期化、およびアクティブ化するシステムサービスです。 このトピックでは、AudioEndpointBuilder サービスによって使用されるアルゴリズムの概要について説明します。

AudioEndpointBuilder サービスは、アルゴリズムを使用してエンドポイントを検出および列挙します。 このアルゴリズムは、多重化された (MUXed) キャプチャデバイスへのシステムアクセスを単純化し、複数のホストピンと複数のブリッジピン (またはその両方) を伴うトポロジを操作できるように設計されています。

Windows XP では、オーディオモデルは、オーディオデバイスという用語を使用して、プラグアンドプレイ (PnP) ツリーで概念デバイスを参照していました。 Windows Vista 以降のバージョンの Windows では、ユーザーが物理的に対話するデバイスをより適切に表現できるように、オーディオデバイスの概念が再設計されています。

Windows Vista、 [Mmdevice api](https://docs.microsoft.com/windows/win32/coreaudio/mmdevice-api) 、および実行[api](https://docs.microsoft.com/windows/win32/coreaudio/wasapi)の2つの新しい api を使用して、これらの新しいオーディオデバイスにアクセスして操作できます。 MMDevice API は、新しいオーディオデバイスをエンドポイントとして参照します。

AudioEndpointBuilder サービスは、デバイスインターフェイスの到着と削除のために[**KSCATEGORY\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-audio)クラスを監視します。 オーディオデバイスドライバーが KSCATEGORY\_audio device インターフェイスクラスの新しいインスタンスを登録すると、AudioEndpointBuilder サービスがデバイスインターフェイス通知を検出し、アルゴリズムを使用してシステム内のオーディオデバイスのトポロジを調べ、適切なアクションを実行します。

次の一覧は、AudioEndpointBuilder で使用されるアルゴリズムのしくみをまとめたものです。

1.  未接続ブリッジピンを検索します。

2.  未接続ブリッジピンのエンドポイントを作成します。 たとえば、AudioEndpointBuilder が、KSNODETYPE\_講演者の PIN カテゴリ GUID を使用して接続されていないブリッジピンを検出すると、このブリッジピンのスピーカーエンドポイントが作成されます。 KSNODETYPE\_講演者とその他のピンカテゴリ guid の詳細については、WinDDK\\&lt;build number&gt;\\inc.\\api の「ksmedia. h」を参照してください。

3.  エンドポイントの既定のプロパティを設定します。 たとえば、AudioEndpointBuilder は、名前、アイコン、およびフォームファクターを設定します。

4.  エンドポイントから、パルスコード変調 (PCM)、audio コーデック-3 (AC3)、または Windows media video (WMV) をサポートするホスト pin までのパスがあるかどうかを判断します。 ホスト pin は KSPIN 構造で、その通信メンバーは\_kspin 通信\_シンクまたは kspin\_通信\_の両方に設定されます。 KSPIN 構造の詳細については、「 [**kspin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)」を参照してください。

5.  エンドポイントの PropertyStore に、オーディオデバイスインターフェイスのレジストリキーのプロパティ情報を設定します。

6.  エンドポイントの状態を設定します。 エンドポイントの状態には、次の3つの値のいずれかを指定できます。

    -   [アクティブ]:  これは、手順 4. で説明したようなパスが存在することを示します。

    -   抜か. オーディオデバイスがジャック検出をサポートしている場合、この状態はエンドポイントのパスが存在することを示し、ジャックはオーディオアダプターの物理コネクタから外されます。

    -   存在しません。 この状態は、手順 4. でパスが見つからなかったことを示しています。このエンドポイントでは、ジャック検出はサポートされていません。

7.  関連付けられている INF ファイルで指定されている場合、このエンドポイントを既定のエンドポイントとして設定します。

エンドポイントが列挙された後、オーディオシステムのクライアントは、新しい Windows Vista Api を使用して (前述のように) 直接操作することも、Wave、 [DirectShow](https://docs.microsoft.com/windows/win32/directshow/directshow) 、DirectSound などの使い慣れた api を使用して間接的に操作することもでき[ます。](https://docs.microsoft.com/previous-versions/windows/desktop/bb318665(v=vs.85)) 新しい API メソッドが提供されました。これにより、オーディオクライアントは、エンドポイントの MMDevice ID で開始し、同じエンドポイントの Wave または DirectSound ID にアクセスできるようになります。

エンドポイントを使用する場合は、次の利点を活用できます。

-   コンピューターを再起動する頻度に関係なく、同じグローバル一意識別子 (GUID) を使用できます。 この永続的な GUID を持つ方が、waveOut ID やエンドポイントのフレンドリ名を保存するよりも信頼性が高くなります。

-   コンピューターを再起動する頻度に関係なく、同じ PropertyStore を使用できます。 オーディオデバイス関連のメタデータは、エンドポイントの PropertyStore に保存されます。

-   多重化 (MUX) と多重化解除 (DEMUX) の pin は、自動的に管理され、AudioEndpointBuilder サービスによって列挙されます。

オーディオデバイスで動作する独自のオーディオデバイスドライバーと INF ファイルを開発し、オーディオアプリケーションを開発する場合、またはその両方を行う場合は、次の問題とベストプラクティスに注意することをお勧めします。 これらの推奨事項を考慮してドライバーとアプリケーションを開発すると、AudioEndpointBuilder でより効果的に機能するドライバー、INF ファイル、およびオーディオクライアントが生成されます。

-   名前付け規則。 エンドポイントに使用される名前付け規則は、ブリッジピンのフレンドリ名に基づいています。 ただし、スピーカーエンドポイントの場合、名前は "スピーカー" にハードコーディングされており、ドライバーやサードパーティ製のアプリケーションでは変更できません。

-   最適でないトポロジ。 特定のトポロジは、AudioEndpointBuilder でエンドポイントを列挙するために使用されるアルゴリズムにより、最適でないと見なされます。 たとえば、これらの最適化されていないトポロジのいずれかを作成する場合は、非表示のエンドポイントを持つホスト pin を作成します。 AudioEndpointBuilder または分割されたエンドポイント (分割エンドポイント) は、AudioEndpointBuilder が関連するホストピンにリンクできません。

    -   **非表示のエンドポイント**

        次の図では、1つのブリッジピン (スピーカー) に接続されている2つのホスト pin を持つ KS フィルターが表示されています。

        ![非表示のエンドポイントを使用した、ac 3 ホスト pin を示す問題のあるトポロジを示す図](images/hidden-endpoint-bad.png)

        AudioEndpointBuilder がこのブリッジピンを検出すると、1つのホストピンに対してのみパスをトレースし、ブリッジ pin の既定値を設定し、スピーカーエンドポイントを作成してアクティブ化し、他のブリッジピンの検出を続けます。 そのため、他のホストの pin は、AudioEndpointBuilder から非表示のままになります。

        ![ホストピンとエンドポイント間の追跡可能なパスで推奨されるトポロジを示す図](images/hidden-endpoint-good.png)

        上の図では、AudioEndpointBuilder が2つのブリッジピン (スピーカーと SPDIF) を表示できるようになったため、AudioEndpointBuilder が2つのホストピン (PCM と AC-3/PCM) を検出できるように、問題のあるトポロジが再設計されています。

    -   **分割**

        1つのホスト pin が複数のブリッジ pin に接続すると、別の種類の最適化されていないトポロジが作成されます。 次の図は、PCM ホストピンがスピーカーブリッジピンと SPDIF ブリッジ pin に接続するトポロジを示しています。

        ![1つのホスト pin に接続されている2つのエンドポイントを示す問題のあるトポロジを示す図](images/splitter-bad.png)

        この場合、AudioEndpointBuilder は1つのブリッジピンを検出し、PCM ホスト pin へのパスをトレースし、既定値を設定して、スピーカーエンドポイントを作成してアクティブ化します。 AudioEndpointBuilder は、次のブリッジピンを検出すると、同じ PCM ホスト pin へのパスをトレースし、既定値を設定して、SPDIF エンドポイントを作成してアクティブ化します。 ただし、両方のエンドポイントが初期化され、アクティブ化されていても、いずれかのエンドポイントにストリーミングしても、相互にストリームすることはできません。言い換えると、これらは相互に排他的なエンドポイントです。

        次の図は、別の接続が存在する、このトポロジの再設計を示しています。 この設計により、AudioEndpointBuilder は、2つのブリッジピンそれぞれについて、PCM ホスト pin へのパスをトレースすることができます。

        ![ホストピンとエンドポイント間の追跡可能なパスで推奨されるトポロジを示す図](images/splitter-good.png)

-   エンドポイントの形式。 オーディオエンジンが共有モードで実行されている場合、エンドポイントの形式は、インストール時に INF ファイルによって指示された特定の設定を前提とします。 たとえば、オーディオデバイスのオーディオドライバーは、関連付けられている INF ファイルを使用して、既定のエンドポイントを 44.1 kHz、16ビット、ステレオ PCM 形式に設定します。 インストール後、エンドポイントの形式を変更するには、コントロールパネルまたはサードパーティのアプリケーションを使用する必要があります。

-   既定のデバイス。 既定のデバイスとして設定されているエンドポイントは、インストール時に INF ファイルの情報を使用して選択されます。 インストールが完了したら、[コントロールパネル] またはサードパーティ製のアプリケーションを使用して、既定のエンドポイントとなる別のエンドポイントを選択する必要があります。

**注:**    INF ファイルで、インストール時に既定として設定するエンドポイントが選択されていない場合、クライアントアプリケーションは mmdevice API を使用してエンドポイントを選択できます。 API は、フォームファクターランクと、エンドポイントがレンダリングエンドポイントとキャプチャエンドポイントのどちらであるかに基づいて選択します。 次の表に、選択の順序を示します。
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ランクのレンダリング</th>
<th align="left">ランクのキャプチャ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Speakers</p></td>
<td align="left"><p>マイク</p></td>
</tr>
<tr class="even">
<td align="left"><p>改行</p></td>
<td align="left"><p>インライン</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SPDIF</p></td>
<td align="left"><p>SPDIF</p></td>
</tr>
</tbody>
</table>

 

 

MMDevice API を使用して既定のエンドポイントを選択し、使用可能なエンドポイントの順位が同じである場合、MMDevice API はエンドポイント Id をアルファベット順にして、既定として選択するエンドポイントを決定します。 たとえば、オーディオアダプターに改行とラインインコネクタの両方があり、関連付けられている INF ファイルでインストール時に既定値として選択されていない場合、MMDevice API は最初にアルファベット順になっているエンドポイント Id を識別し、そのコネクタを既定値として設定します。 この選択は、エンドポイント Id が永続的であるため、システムを再起動した後も保持されます。 ただし、高いランクのエンドポイント (たとえば、マイクコネクタを使用する2番目のアダプター) がシステムに表示されている場合、選択は保持されません。

 

 




