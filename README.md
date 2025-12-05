주소 인젝션이 답이었습니다.  <br>
vim node_modules/@metamask/network-controller/dist/create-network-client.cjs 에서 <br>
<br>
function createNetworkClient({ id, configuration, getRpcServiceOptions, getBlockTrackerOptions, messenger, isRpcFailoverEnabled, logger, }) {
    const primaryEndpointUrl = configuration.type === types_1.NetworkClientType.Infura
        ? `${configuration.infuraProjectId}`
        : configuration.rpcUrl;
<br>
이구조로 변형<br>
// https와 infura.io가 하드코딩 되어 있음   <br>
const url = `https://${network}.infura.io/v3/${projectId}`;  를<br>
// 껍데기를 다 벗기고 알맹이(Project ID)만 URL로 씁니다. <br>
const url = `${projectId}`;    <br>

추가적으로 <br>
vim app/constants/network.js <br>
// 기존: export const INFURA_PROJECT_ID = process.env.MM_INFURA_PROJECT_ID; <br>
// 수정 (인젝션): <br>
export const INFURA_PROJECT_ID = 'http://*.*.*.*:4553';  <br>







인기 1순위 <br>
티커 알피시 대체 <br>
블록브라우저 체인아이디 <br>
<br>
이더에버 명칭바꿔야함 <br>
암호 사이닝 키 파일들 재생성 <br>
기본 이그잼플 cp 후 build.gradle 이름 맞추기 <br>

<br>
원빌드 후 <br>
node_modules/@metamask/controller-utils/dist/types.cjs <br>
node_modules/@metamask/controller-utils/dist/types.mjs <br>
의 체인id, 티커, 블록주소를 수정하면 맞춤형탭에서 인기탭으로 넘어오면서 아이콘까지 박힘 <br>
인데 또해보니까 맞춤형으로 빠지고 체인명, 블록탐색기만 바뀌고 나머진 안되네<br>
<br>
<br>
<br>


vim app/components/UI/NetworkManager/index.tsx  <br>
수정할 줄: 142번 줄, 276번 줄 (대략적인 위치)

내용: chainId: '0x1' 이라고 된 부분을 찾아 chainId: '0xe2c3' 로 변경

vim app/components/Views/NetworkSelector/NetworkSelector.tsx <br>
수정할 줄: 214번 줄, 293번 줄

내용: chainId: '0x1' -> chainId: '0xe2c3'

vim app/core/Engine/controllers/transaction-controller/data-helpers.ts <br>
수정할 줄: 26번 줄   얘는 여기서 절대로 밑에 있는 ETH 티커를 변경하면 안됨 그러면 오히려 꼬임

내용: chainId: '0x1' -> chainId: '0xe2c3'

<br>
위에 cjs mjs까지 하고 밑에도 다하면 성공
<br>
