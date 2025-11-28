
import streamlit as st

# 1. 앱 설정 및 제목
st.set_page_config(page_title="친구 연락 앱", page_icon="💬")
st.title("친구 채팅 앱 💬")

# 2. 채팅 기록을 저장할 session_state 초기화
# 'messages'라는 키가 session_state에 없으면 빈 리스트로 초기화합니다.
if "messages" not in st.session_state:
    st.session_state.messages = []

# 3. 사용자 이름 설정 (앱을 사용할 때마다 사용자 이름을 받습니다)
# 'username'이 session_state에 없으면 입력 필드를 보여줍니다.
if "username" not in st.session_state or not st.session_state.username:
    
    # 사용자 이름을 입력받는 섹션
    with st.empty():
        user_name_input = st.text_input("당신의 이름을 입력해주세요:", key="initial_name_input")
        
        if user_name_input:
            st.session_state.username = user_name_input
            # 이름이 설정되면 입력 필드를 제거합니다.
            st.rerun() 
            
# 사용자 이름이 설정된 경우에만 채팅 인터페이스를 표시
if "username" in st.session_state and st.session_state.username:
    st.write(f"환영합니다, **{st.session_state.username}**님!")
    
    # 4. 저장된 채팅 기록 표시
    for message in st.session_state.messages:
        # 메시지의 role(사용자 이름)에 따라 메시지 박스를 표시합니다.
        with st.chat_message(message["role"]):
            st.markdown(message["content"])

    # 5. 새 메시지 입력 처리
    # st.chat_input은 사용자 입력을 처리하는 전용 위젯입니다.
    if prompt := st.chat_input("메시지를 입력하세요..."):
        
        # 새 메시지 객체 생성 (현재 사용자 이름과 입력 내용 포함)
        new_message = {"role": st.session_state.username, "content": prompt}
        
        # 5-1. 세션 상태에 메시지 추가 (데이터 저장)
        st.session_state.messages.append(new_message)
        
        # 5-2. 화면에 새 메시지 즉시 표시
        with st.chat_message(st.session_state.username):
            st.markdown(prompt)
