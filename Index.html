<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SC&U 이동 약자 맞춤형 스마트 지도 - 카카오 지도 네비게이션 (V5.0)</title>
    
    <!-- React & Babel Loaders -->
    <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Kakao Map API -->
    <script type="text/javascript" src="//dapi.kakao.com/v2/maps/sdk.js?appkey=c03d64c5480003c0435d50749525c215&libraries=services,clusterer,drawing"></script>
    
    <link rel="stylesheet" href="styles.css">
</head>
<body class="bg-gray-100 h-screen font-sans">
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect, useRef } = React;

        // ========== 설정 및 상수 ==========
        const CONFIG = {
            mapCenter: { lat: 37.2808, lng: 127.0099 }, // 경주지역 기본좌표
            zoomLevel: 4,
            destination: 'E6 건물',
            destinationCoord: { lat: 37.2808, lng: 127.0099 }
        };

        const PHASE_META = {
            INIT: { 
                title: '대기 중', 
                desc: '목적지를 설정하고 안내를 시작하세요.',
                icon: '🗺️' 
            },
            DEST_CONFIRM: { 
                title: '3-1. 이동 시작', 
                desc: 'E6 건물로 안내를 준비합니다.',
                icon: '📍' 
            },
            LOC_AUTH: { 
                title: '3-1. 이동 시작', 
                desc: '경로 탐색이 완료되었습니다.',
                icon: '✓' 
            },
            NAV_1: { 
                title: '이동 중...', 
                desc: '목적지로 이동하고 있습니다.',
                icon: '🚗' 
            },
            OBS_1: { 
                title: '3-2. 1차 장애물 감지', 
                desc: '전방에 장애물이 제보되었습니다.',
                icon: '🚨' 
            },
            NAV_2: { 
                title: '기존 경로 유지', 
                desc: '장애물 경고를 무시하고 기존 경로로 이동합니다.',
                icon: '→' 
            },
            OBS_2: { 
                title: '3-2. 2차 장애물 감지', 
                desc: '전방에 도로 정비 공사가 진행 중입니다.',
                icon: '🚧' 
            },
            NAV_END: { 
                title: '목적지 접근 중', 
                desc: 'E6 건물에 거의 도착했습니다.',
                icon: '📍' 
            },
            ARRIVED_PROMPT: { 
                title: '목적지 도달', 
                desc: '목적지 부근에 도착했습니다.',
                icon: '🏁' 
            },
            ARRIVED: { 
                title: '3-3. 도착 및 주차', 
                desc: '주차장 탐색을 시작합니다.',
                icon: '🅿️' 
            },
            PARKING_SEARCH: { 
                title: '주차장 안내', 
                desc: '지정된 주차 구역의 상태를 확인하세요.',
                icon: '🅿️' 
            },
            DONE: { 
                title: '이용 종료', 
                desc: '주차가 완료되었습니다.',
                icon: '🎉' 
            }
        };

        // 경로 세그먼트 정의
        const ROUTE_SEGMENTS = {
            s1: {
                coords: [
                    { lat: 37.2808, lng: 127.0099 },
                    { lat: 37.2815, lng: 127.0110 }
                ],
                duration: 2.5,
                nextPhase: 'OBS_1'
            },
            s2: {
                coords: [
                    { lat: 37.2815, lng: 127.0110 },
                    { lat: 37.2825, lng: 127.0120 }
                ],
                duration: 1.5,
                nextPhase: 'OBS_2'
            },
            s3: {
                coords: [
                    { lat: 37.2825, lng: 127.0120 },
                    { lat: 37.2835, lng: 127.0130 }
                ],
                duration: 1.0,
                nextPhase: 'ARRIVED_PROMPT'
            },
            s4: {
                coords: [
                    { lat: 37.2835, lng: 127.0130 },
                    { lat: 37.2840, lng: 127.0135 }
                ],
                duration: 0.8,
                nextPhase: 'ARRIVED'
            }
        };

        const OBSTACLES = {
            obs1: {
                coord: { lat: 37.2815, lng: 127.0110 },
                title: '1차 장애물 (전방 장애물)',
                desc: '전방에 장애물이 제보되었습니다.',
                phase: 'OBS_1'
            },
            obs2: {
                coord: { lat: 37.2825, lng: 127.0120 },
                title: '2차 장애물 (도로 정비)',
                desc: '도로 정비 공사가 진행 중입니다.',
                phase: 'OBS_2'
            }
        };

        // ========== 상태 보드 컴포넌트 ==========
        const StatusCard = ({ phase }) => {
            const meta = PHASE_META[phase] || PHASE_META.INIT;
            return (
                <div className="card status-board">
                    <h2 className="card-header">상태 보드</h2>
                    <div className="card-content">
                        <div className="status-display">
                            <span className="status-badge">{meta.icon} {phase}</span>
                            <h3 className="status-title">{meta.title}</h3>
                            <p className="status-desc">{meta.desc}</p>
                        </div>
                    </div>
                </div>
            );
        };

        // ========== 제어 패널 컴포넌트 ==========
        const ControlPanel = ({ phase, onPhaseChange }) => {
            return (
                <div className="card">
                    <h2 className="card-header">제어 패널</h2>
                    <div className="card-content control-panel">
                        {phase === 'INIT' && (
                            <div className="text-center">
                                <p className="mb-4 font-semibold text-gray-700">E6 건물로 이동하시겠습니까?</p>
                                <button 
                                    onClick={() => onPhaseChange('DEST_CONFIRM')} 
                                    className="btn btn-primary btn-block">
                                    ✓ 예
                                </button>
                            </div>
                        )}

                        {phase === 'DEST_CONFIRM' && (
                            <button 
                                onClick={() => onPhaseChange('LOC_AUTH')} 
                                className="btn btn-success btn-block">
                                📍 위치 권한 허용
                            </button>
                        )}

                        {phase === 'LOC_AUTH' && (
                            <button 
                                onClick={() => onPhaseChange('NAV_1')} 
                                className="btn btn-primary btn-block btn-pulse">
                                🚗 경로 안내 시작
                            </button>
                        )}

                        {phase === 'OBS_1' && (
                            <div className="control-section danger">
                                <p className="control-section-title">🚨 1차 장애물</p>
                                <p className="text-sm text-red-700 mb-3">전방에 장애물이 제보되었습니다.</p>
                                <button 
                                    disabled
                                    className="btn btn-primary btn-block mb-2"
                                    style={{opacity: 0.5, cursor: 'not-allowed'}}>
                                    대체 경로 우회 (비활성화)
                                </button>
                                <button 
                                    onClick={() => onPhaseChange('NAV_2')} 
                                    className="btn btn-primary btn-block">
                                    ✅ 기존 경로로 계속 이동
                                </button>
                            </div>
                        )}

                        {phase === 'OBS_2' && (
                            <div className="control-section danger">
                                <p className="control-section-title">🚧 2차 장애물</p>
                                <p className="text-sm text-red-700 mb-3">도로 정비 공사가 진행 중입니다.</p>
                                <button 
                                    disabled
                                    className="btn btn-primary btn-block mb-2"
                                    style={{opacity: 0.5, cursor: 'not-allowed'}}>
                                    대체 경로 우회 (비활성화)
                                </button>
                                <button 
                                    onClick={() => onPhaseChange('NAV_END')} 
                                    className="btn btn-primary btn-block">
                                    ✅ 기존 경로로 계속 이동
                                </button>
                            </div>
                        )}

                        {phase === 'ARRIVED_PROMPT' && (
                            <button 
                                onClick={() => onPhaseChange('ARRIVED')} 
                                className="btn btn-success btn-block">
                                🏁 목적지 도착 확인
                            </button>
                        )}

                        {phase === 'ARRIVED' && (
                            <button 
                                onClick={() => onPhaseChange('PARKING_SEARCH')} 
                                className="btn btn-primary btn-block">
                                🅿️ 주변 주차장 안내 켜기
                            </button>
                        )}

                        {phase === 'PARKING_SEARCH' && (
                            <div className="control-section info">
                                <p className="control-section-title">🅿️ 주차장 안내</p>
                                <p className="text-sm text-blue-700 mb-3">
                                    지도에서 3개의 주차 칸 상태를 확인하세요.<br/>
                                    (가장 좌측 자리 선택 가능)
                                </p>
                                <button 
                                    onClick={() => onPhaseChange('DONE')} 
                                    className="btn btn-success btn-block">
                                    ✅ 빈 주차자리에 주차 완료
                                </button>
                            </div>
                        )}

                        {phase === 'DONE' && (
                            <div className="text-center p-4">
                                <p className="text-4xl mb-2">🎉</p>
                                <p className="font-bold text-gray-800 mb-4 text-lg">
                                    주차가 완료되었습니다!
                                </p>
                                <button 
                                    onClick={() => window.location.reload()} 
                                    className="btn btn-outline btn-block">
                                    🔄 데모 다시 시작
                                </button>
                            </div>
                        )}
                    </div>
                </div>
            );
        };

        // ========== 주차 패널 컴포넌트 ==========
        const ParkingPanel = ({ onPark }) => {
            return (
                <div className="parking-panel">
                    <p className="parking-header">🅿️ 주차 구역 선택 (3개 슬롯)</p>
                    <div className="parking-slots">
                        <div className="parking-slot" onClick={() => onPark(0)}>
                            <div className="slot-label available">주차자리 있음</div>
                            <div className="slot-visual available">✓</div>
                        </div>
                        <div className="parking-slot">
                            <div className="slot-label construction">1번 공사중</div>
                            <div className="slot-visual construction">1</div>
                        </div>
                        <div className="parking-slot">
                            <div className="slot-label occupied">2번 사용중</div>
                            <div className="slot-visual occupied">2</div>
                        </div>
                    </div>
                </div>
            );
        };

        // ========== 지도 컴포넌트 ==========
        const KakaoMapComponent = ({ 
            phase, 
            currentPosition, 
            route, 
            obstacles,
            onMapInit 
        }) => {
            const mapContainer = useRef(null);
            const mapRef = useRef(null);
            const markersRef = useRef([]);
            const polylinesRef = useRef([]);

            useEffect(() => {
                if (!mapContainer.current) return;

                // 카카오 지도 초기화
                const container = mapContainer.current;
                const options = {
                    center: new kakao.maps.LatLng(CONFIG.mapCenter.lat, CONFIG.mapCenter.lng),
                    level: CONFIG.zoomLevel
                };
                
                const map = new kakao.maps.Map(container, options);
                mapRef.current = map;
                
                onMapInit(map);

                return () => {
                    // Cleanup
                    markersRef.current.forEach(marker => marker.setMap(null));
                    polylinesRef.current.forEach(polyline => polyline.setMap(null));
                };
            }, [onMapInit]);

            // 경로 그리기
            useEffect(() => {
                if (!mapRef.current || !route || route.length === 0) return;

                // 기존 polyline 제거
                polylinesRef.current.forEach(pl => pl.setMap(null));
                polylinesRef.current = [];

                // 새 경로 그리기
                const polyline = new kakao.maps.Polyline({
                    path: route.map(coord => new kakao.maps.LatLng(coord.lat, coord.lng)),
                    strokeWeight: 4,
                    strokeColor: '#22c55e',
                    strokeOpacity: 0.8,
                    strokeStyle: 'solid'
                });
                
                polyline.setMap(mapRef.current);
                polylinesRef.current.push(polyline);
            }, [route]);

            // 현재 위치 마커 업데이트
            useEffect(() => {
                if (!mapRef.current || !currentPosition) return;

                // 기존 마커 제거
                markersRef.current.forEach(marker => marker.setMap(null));
                markersRef.current = [];

                // 현재 위치 마커
                const userMarker = new kakao.maps.Marker({
                    position: new kakao.maps.LatLng(currentPosition.lat, currentPosition.lng),
                    title: '현재 위치',
                    image: new kakao.maps.MarkerImage(
                        'data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%232563eb"><circle cx="12" cy="12" r="10" fill="%232563eb"/><circle cx="12" cy="12" r="6" fill="white"/></svg>',
                        new kakao.maps.Size(30, 30),
                        { offset: new kakao.maps.Point(15, 15) }
                    )
                });
                
                userMarker.setMap(mapRef.current);
                markersRef.current.push(userMarker);

                // 목적지 마커
                const destMarker = new kakao.maps.Marker({
                    position: new kakao.maps.LatLng(CONFIG.destinationCoord.lat, CONFIG.destinationCoord.lng),
                    title: CONFIG.destination,
                    image: new kakao.maps.MarkerImage(
                        'data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%2322c55e"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.42 0-8-3.58-8-8s3.58-8 8-8 8 3.58 8 8-3.58 8-8 8z"/><circle cx="12" cy="12" r="3" fill="%2322c55e"/></svg>',
                        new kakao.maps.Size(35, 35),
                        { offset: new kakao.maps.Point(17.5, 17.5) }
                    )
                });
                
                destMarker.setMap(mapRef.current);
                markersRef.current.push(destMarker);

                // 지도 중심을 현재 위치로 이동
                mapRef.current.setCenter(
                    new kakao.maps.LatLng(currentPosition.lat, currentPosition.lng)
                );
            }, [currentPosition]);

            // 장애물 마커 표시
            useEffect(() => {
                if (!mapRef.current) return;

                obstacles.forEach(obs => {
                    const obsMarker = new kakao.maps.Marker({
                        position: new kakao.maps.LatLng(obs.coord.lat, obs.coord.lng),
                        title: obs.title,
                        image: new kakao.maps.MarkerImage(
                            'data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23dc2626"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-2h2v2zm0-4h-2V7h2v6z"/></svg>',
                            new kakao.maps.Size(35, 35),
                            { offset: new kakao.maps.Point(17.5, 17.5) }
                        )
                    });
                    
                    obsMarker.setMap(mapRef.current);
                    markersRef.current.push(obsMarker);

                    // 정보 창
                    const infoWindow = new kakao.maps.InfoWindow({
                        content: `<div style="padding:12px; font-size:12px; background:white; border-radius:4px;">
                            <strong>${obs.title}</strong><br/>
                            ${obs.desc}
                        </div>`
                    });
                    
                    kakao.maps.event.addListener(obsMarker, 'click', () => {
                        infoWindow.open(mapRef.current, obsMarker);
                    });
                });
            }, [obstacles]);

            return <div ref={mapContainer} className="map-container" id="kakao-map" />;
        };

        // ========== 메인 앱 컴포넌트 ==========
        const App = () => {
            const [phase, setPhase] = useState('INIT');
            const [currentPosition, setCurrentPosition] = useState(CONFIG.mapCenter);
            const [route, setRoute] = useState([]);
            const [obstaclesVisible, setObstaclesVisible] = useState([]);

            const handlePhaseChange = (newPhase) => {
                setPhase(newPhase);

                // 각 페이즈별 처리
                switch(newPhase) {
                    case 'NAV_1':
                        animateRoute('s1');
                        break;
                    case 'NAV_2':
                        animateRoute('s2');
                        break;
                    case 'NAV_END':
                        animateRoute('s3');
                        break;
                    case 'OBS_1':
                        setObstaclesVisible([OBSTACLES.obs1]);
                        break;
                    case 'OBS_2':
                        setObstaclesVisible([OBSTACLES.obs2]);
                        break;
                    case 'ARRIVED':
                        setObstaclesVisible([]);
                        break;
                    default:
                        break;
                }
            };

            const animateRoute = (segmentKey) => {
                const segment = ROUTE_SEGMENTS[segmentKey];
                if (!segment) return;

                setRoute(segment.coords);
                
                // 위치 애니메이션
                const startPos = segment.coords[0];
                const endPos = segment.coords[segment.coords.length - 1];
                const steps = 30;
                let currentStep = 0;

                const animate = () => {
                    currentStep++;
                    const progress = currentStep / steps;
                    
                    const newLat = startPos.lat + (endPos.lat - startPos.lat) * progress;
                    const newLng = startPos.lng + (endPos.lng - startPos.lng) * progress;
                    
                    setCurrentPosition({ lat: newLat, lng: newLng });

                    if (currentStep < steps) {
                        setTimeout(animate, (segment.duration * 1000) / steps);
                    } else {
                        setCurrentPosition(endPos);
                        setTimeout(() => {
                            setPhase(segment.nextPhase);
                        }, 500);
                    }
                };

                animate();
            };

            return (
                <div className="main-layout">
                    <div className="sidebar">
                        <StatusCard phase={phase} />
                    </div>

                    <div className="map-area">
                        <KakaoMapComponent 
                            phase={phase}
                            currentPosition={currentPosition}
                            route={route}
                            obstacles={obstaclesVisible}
                            onMapInit={() => {}}
                        />
                        {phase === 'PARKING_SEARCH' && (
                            <ParkingPanel onPark={() => setPhase('DONE')} />
                        )}
                    </div>

                    <div className="sidebar">
                        <ControlPanel phase={phase} onPhaseChange={handlePhaseChange} />
                    </div>
                </div>
            );
        };

        // React 렌더링
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
