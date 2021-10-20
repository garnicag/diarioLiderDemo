<template>
  <div class="container">
    <CBox
      v-bind="mainStyles[colorMode]"
      d="flex"
      w="100vw"
      h="100vh"
      flex-dir="column"
      justify-content="center"
    > 
      <CBox align="center">
        <img src="/logo.png" alt="Diario Líder" />
      </CBox>
      <CHeading size="lg" text-align="center" mt="20" mb="4">
        Ingreso de usuario
      </CHeading>
      <CFlex justify="center" direction="column" align="center">
        <CAvatarGroup>
          <CAvatar w="150px" h="150px" />
        </CAvatarGroup>

        <CBox mt="5">
          <CInput placeholder="Nombre de usuario" size="lg" v-model="username" />
          <CInput type="password" placeholder="Contraseña" v-model="password" size="lg" />
        </CBox>

        <CBox mt="5">
          <CButton
            variant-color="blue"
            @click="login"
          >
            Ingresar
          </CButton>
          <CButton
            variant-color="red"
            @click="forgotPassword"
          >
            Olvidó su contraseña
          </CButton>
        </CBox>
        
        <CModal :is-open="showModal">
          <CModalOverlay />
          <CModalContent>
            <CModalHeader>Are you sure?</CModalHeader>
            <CModalBody>Deleting user cannot be undone</CModalBody>
            <CModalFooter>
              <CButton @click="showModal = false">
                Cancel
              </CButton>
              <CButton
                margin-left="3"
                variant-color="red"
                @click="showModal = false"
              >
                Delete User
              </CButton>
            </CModalFooter>
            <CModalCloseButton @click="showModal = false" />
          </CModalContent>
        </CModal>
      </CFlex>
    </CBox>
  </div>
</template>

<script lang="js">
import {
  CBox,
  CButton,
  CAvatarGroup,
  CAvatar,
  CModal,
  CModalContent,
  CModalOverlay,
  CModalHeader,
  CModalFooter,
  CModalBody,
  CModalCloseButton,
  CHeading,
  CFlex,
  CInput
} from '@chakra-ui/vue'

export default {
  name: 'App',
  components: {
    CBox,
    CButton,
    CAvatarGroup,
    CAvatar,
    CModal,
    CModalContent,
    CModalOverlay,
    CModalHeader,
    CModalFooter,
    CModalBody,
    CModalCloseButton,
    CFlex,
    CHeading,
    CInput
  },
  inject: ['$chakraColorMode', '$toggleColorMode'],
  data () {
    return {
      showModal: false,
      mainStyles: {
        dark: {
          bg: 'gray.700',
          color: 'whiteAlpha.900'
        },
        light: {
          bg: 'white',
          color: 'gray.900'
        }
      },
      username: '',
      password: ''
    }
  },
  computed: {
    colorMode () {
      return this.$chakraColorMode()
    },
    theme () {
      return this.$chakraTheme()
    },
    toggleColorMode () {
      return this.$toggleColorMode
    }
  },
  methods: {
    forgotPassword() {
      this.$toast({
        title: 'Solicitud de contraseña',
        description: "Enviamos una contraseña nueva al correo electrónico",
        status: 'success',
        duration: 10000,
        isClosable: true
      })
    },
    login() {
      if (this.username === 'demo' && this.password === '12345678') {
        this.$toast({
          title: 'Ingresando al CMS',
          description: "Por favor espere",
          status: 'success',
          duration: 10000,
          isClosable: true
        })
      } else {
        this.$toast({
          title: 'Credenciales incorrectas',
          description: "Nombre de usuario y contraseña errados, intente de nuevo",
          status: 'error',
          duration: 10000,
          isClosable: true
        })
      }
    }
  }
}
</script>
