<template>
	<v-app>

		<v-content>

			<v-container>

				<v-row align="center" justify="center">
					<v-col sm="4" style="display: flex; justify-content: center">
						<v-img
							class="mx-2"
							src="img/bar/muni.png"
							
							max-width="200"
							contain
						></v-img>
					</v-col>
					<v-col sm="4" style="display: flex; justify-content: center">
						<v-img
							class="mx-2"
							src="img/bar/ave.png"
							
							max-width="200"
							contain
						></v-img>
					</v-col>
					<v-col sm="4" style="display: flex; justify-content: center">
						<v-img
							src="img/bar/4f.png"
							
							max-width="150"
							
						></v-img>
					</v-col>
				</v-row>

				<v-stepper v-model="e1" >
					<v-stepper-header>
						<v-stepper-step :complete="e1 > 1" step="1">Registro</v-stepper-step>
						<v-divider></v-divider>
						<v-stepper-step :complete="e1 > 2" step="2">Instalación de la Aplicación</v-stepper-step>
						<v-divider></v-divider>
						<v-stepper-step :complete="e1 > 3" step="3">Información del Evento</v-stepper-step>
						<v-divider></v-divider>
					</v-stepper-header>
					<v-stepper-items>

						<!-- Paso 1 -->

						<v-stepper-content  step="1">

							<v-row>
								<v-col>
									<h4>Paso 1 de 3</h4>
								</v-col>
							</v-row>

							<v-form ref="form" v-model="valid">

								<v-row>

									<v-col cols="12" sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-account-circle" hide-details outlined label="Nombres" autocomplete="off" v-model="usuario.NOMBRE" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-account-circle" hide-details outlined label="Apellidos" autocomplete="off" v-model="usuario.APELLIDO" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-account-card-details" hide-details outlined label="DPI" autocomplete="off" v-model="usuario.DPI" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12"  sm="6" md="6">
										<v-autocomplete dense prepend-icon="mdi-office-building" hide-details outlined label="Tipo de Inmueble" :items="tipos_inmuebles" autocomplete="off" v-model="usuario.TIPO_INMUEBLE" :rules="[v => !!v || 'Item is required']" required></v-autocomplete>
									</v-col>
									<v-col cols="12"  sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-office-building" hide-details outlined label="No. de Niveles del Inmueble" autocomplete="off" v-model="usuario.NIVELES" :rules="[v => !!v || 'Item is required']" type="number" required></v-text-field>
									</v-col>
									<!-- <v-col cols="12"  sm="6" md="6">
										<v-autocomplete dense prepend-icon="mdi-clipboard-list" hide-details outlined label="Hipótesis" :items="components" autocomplete="off" v-model="usuario.hipotesis"></v-autocomplete>
									</v-col> -->
									<v-col cols="12"  sm="6" md="6" >
										<strong >El tipo de institución del inmueble es:</strong>
										<v-radio-group center class="text-center" style="margin-top: 0px" hide-details row v-model="usuario.TIPO_INSTITUCION" :rules="[v => !!v || 'Item is required']" required>
											<v-radio label="Público" value="1"></v-radio>
											<v-radio label="Privado" value="2"></v-radio>
										</v-radio-group>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense hide-details prepend-icon="mdi-office-building" outlined label="Nombre de la Institución/Dependencia/Empresa" autocomplete="off" v-model="usuario.NOMBRE_INSTITUCION" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-account-group" hide-details outlined label="Cantidad de Personal Fijo" autocomplete="off" v-model="usuario.PERSONAL_FIJO" type="number"></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-account-group" hide-details outlined label="Cantidad de Visitantes" type="number" autocomplete="off" v-model="usuario.PERSONAL_TEMPORAL" ></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-account-group" hide-details outlined label="Cantidad de Personas con Discapacidad" autocomplete="off" v-model="usuario.PERSONAS_DISCAPACIDAD" type="number"></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="12">
										<strong>Dirección del Inmueble</strong>
									</v-col>
									<v-col cols="12"  sm="6" md="6">
										<v-autocomplete dense prepend-icon="mdi-map-marker"  hide-details outlined label="Zona" :items="zonas" autocomplete="off" v-model="usuario.ZONA" :rules="[v => !!v || 'Item is required']" required></v-autocomplete>
									</v-col>
									<v-col cols="12"  sm="6" md="6">
										<v-text-field dense prepend-icon="mdi-map-marker" hide-details outlined label="Colonia"  autocomplete="off" v-model="usuario.COLONIA" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12"  sm="6" md="12">
										<v-text-field dense prepend-icon="mdi-map-marker" hide-details outlined label="Dirección" :items="components" autocomplete="off" v-model="usuario.DIRECCION" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12" sm="12" md="12">
										<strong>Ingresa un correo y número telefonico para poder dar seguimiento y tener un medio de comunicación donde se enviará información relevante.  Asegúrate de escribirlo corréctamente.</strong>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense hide-details prepend-icon="mdi-email" outlined label="Correo Electrónico" autocomplete="off" v-model="usuario.EMAIL" type="email" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense hide-details prepend-icon="mdi-phone" outlined label="Teléfono" autocomplete="off" v-model="usuario.TELEFONO" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense hide-details prepend-icon="mdi-lock" outlined label="Contraseña" autocomplete="off" v-model="usuario.PASS" :append-icon="show1 ? 'mdi-eye-off' : 'mdi-eye'" @click:append="show1 = !show1" :type="show1 ? 'text' : 'password'" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>
									<v-col cols="12" sm="6" md="6">
										<v-text-field dense hide-details prepend-icon="mdi-lock" outlined label="Repita su contraseña" autocomplete="off" v-model="usuario.REPITE_PASS" :append-icon="show2 ? 'mdi-eye-off' : 'mdi-eye'" @click:append="show2 = !show2" :type="show2 ? 'text' : 'password'" :rules="[v => !!v || 'Item is required']" required></v-text-field>
									</v-col>

									<v-col cols="12" sm="12" md="12">
										<v-alert
										border="top"
										colored-border
										type="info"
										elevation="2"
										>
											<strong>Cualquier duda o consulta comunicarse al número 22858628 o enviar un correo electronico a eitorres@muniguate.com / crossi@muniguate.com / lmlopez@muniguate.com</strong>
										</v-alert>
										
									</v-col>

								</v-row>

							</v-form>

							<v-row class="mt-4">
								<v-col cols="12" lg="9" md="6" sm="6">
									<v-btn color="primary" :loading="registrando" :disabled="registrando" @click="registrar_usuario">
										Continuar
									</v-btn>

									<v-btn text @click="cancelar">Cancelar</v-btn>
								</v-col>
								<v-col cols="12" lg="3" md="6" sm="6">
									<v-btn text  color="primary" @click="ya_registrado">
										YA ESTOY REGISTRADO
									</v-btn>
								</v-col>
							</v-row>
						</v-stepper-content>

						<!-- Paso 2 -->

						<v-stepper-content step="2">

							<v-row>
								<v-col>
									<h4>Paso 2 de 3</h4>
								</v-col>
							</v-row>

							<v-row>
								<v-col v-if="!registrado">
									<v-alert border="top"
									colored-border
									type="success"
									elevation="2" 
									v-if="persona">
										Excelente el proceso de registro ha sido exitoso.  Para continuar deberá seguir las instrucciones que se le muestran a continuación para la instalación de la aplicación AVE Ciudad e iniciar sesión con el correo registrado <strong>{{ persona.email }}</strong> y la contraseña seleccionada.
									</v-alert>
								</v-col>

								<v-col v-if="registrado">
									<v-alert border="top"
									colored-border
									type="success"
									elevation="2" 
									v-if="persona">
										Excelente ha sido agregado al <strong>MACRO SIMULACRO 4F</strong>.    Hemos detectado que ya se encuentra registrado en la aplicación AVE Ciudad por lo que deberá iniciar sesión siguiendo las instrucciones que se le muestran a continuación.
										<!-- Excelente el proceso de registro ha sido exitoso.  Para continuar deberá seguir las instrucciones que se le muestra a continuación para la instalación de la aplicación AVE Ciudad e iniciar sesión con el correo registrado <strong>{{ persona.email }}</strong> y la contraseña seleccionada. -->
									</v-alert>
								</v-col>
								
							</v-row>

							<v-row>
								<v-col>
									<h2 class="text-center">Seleccione el sistema operativo de su teléfono: </h2>
								</v-col>
							</v-row>
							<v-row justify="center" align="center" class="text-center">
								<v-col lg="2" sm="6">
									<v-card hover class="mx-auto" :color="os == 'android' ? '#385F73' : 'white'" :dark="os == 'android' ? true : false" @click="select_android">
										<v-card-text>
											<strong>Android (Otros)</strong>
										</v-card-text>
										<v-container style="display: flex; justify-content: center">
											<v-img
												src="img/android.png"
												max-width="100"
											></v-img>
										</v-container>
									</v-card>
									
								</v-col>
								<v-col sm="6" lg="2">
									<v-card hover class="mx-auto" :color="os == 'ios' ? '#385F73' : 'white'" :dark="os == 'ios' ? true : false" @click="select_ios">
										<v-card-text>
											<strong>iOS (iPhone)</strong>
										</v-card-text>
										<v-container style="display: flex; justify-content: center">
											<v-img
												src="img/apple.png"
												max-width="100"
											></v-img>
										</v-container>
									</v-card>
								</v-col>
							</v-row>

							<v-row>
								<v-col>
									<v-stepper vertical v-model="install_counter" v-if="os == 'android'">
										
										<!-- Paso 1 -->

										<v-stepper-step :complete="install_counter > 1"  step="1">
											Ingresar a Google Play

										</v-stepper-step>

										<v-stepper-content step="1">

											<!-- Contenido -->

											<v-row>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/android/paso1.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p><strong>Ubicar Google Play en su dispositivo.</strong></p>
													
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/android/paso2.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p>
														<strong>
															Ingresar a Google Play.
														</strong>
													</p>
													
												</v-col>
											</v-row>

											
											<v-row class="mt-4">
												<v-col>
													<v-btn color="primary" @click="install_counter = 2">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

										<!-- Paso 2 -->

										<v-stepper-step :complete="install_counter > 2" step="2">
											Buscar la aplicación AVE Ciudad
										</v-stepper-step>

										<v-stepper-content step="2">

											<!-- Contenido -->

											<v-row >
												<v-col cols="12" lg="4" sm="12">
													<v-img
														src="img/android/paso3.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p ><strong>En el campo de búsqueda superior ingresar AVE Ciudad.</strong></p>
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12">
													<v-img
														src="img/android/paso4.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p >
														<strong>
															Seleccionar el primer resultado mostrado. 
														</strong>
													</p>
												</v-col>
											</v-row>

											<v-row class="mt-4">
												<v-col>
													<v-btn text @click="install_counter = 1">Atrás</v-btn>

													<v-btn color="primary" @click="install_counter = 3">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

										<!-- Paso 3 -->

										<v-stepper-step :complete="install_counter > 3" step="3" >
											Dar clic en Instalar y esperar
										</v-stepper-step>

										<v-stepper-content step="3">

											<!-- Contenido -->
											<v-row >
												<v-col cols="12" lg="4" sm="12">
													<v-img
														src="img/android/paso5.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p ><strong>Dar clic en el botón Instalar.</strong></p>
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12">
													<v-img
														src="img/android/paso6.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p >
														<strong>
															Esperar a que la aplicación sea descargada e instalada en su dispositivo. 
														</strong>
													</p>
												</v-col>
											</v-row>

											<v-row class="mt-4">
												<v-col>
													<v-btn text @click="install_counter = 2">Atrás</v-btn>

													<v-btn color="primary" @click="install_counter = 4">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

										<!-- Paso 4 -->

										<v-stepper-step :complete="install_counter > 4" step="4" >
											Ingresar a la aplicación e iniciar sesión.
										</v-stepper-step>

										<v-stepper-content step="4">

											<!-- Contenido -->
											<v-row >
												<v-col cols="12" lg="4" sm="12">
													<v-img
														src="img/android/paso7.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p ><strong>Ubicar la aplicación AVE Ciudad en su teléfono.</strong></p>
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12">
													<v-img
														src="img/android/paso8.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p >
														<strong>
															Ingresar el correo eléctronico con el cual se registro así como su contraseña y presionar INICIA SESIÓN. 
														</strong>
													</p>
												</v-col>
											</v-row>

											<v-row class="mt-4">
												<v-col>
													<v-btn text @click="install_counter = 3">Atrás</v-btn>

													<v-btn color="primary" @click="install_counter = 5">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

									</v-stepper>

									<!-- iOS -->

									<v-stepper v-model="install_counter_ios" vertical v-if="os == 'ios'">
										<v-stepper-step step="1" :complete="install_counter_ios > 1">
											Ingrese al App Store
										</v-stepper-step>

										<v-stepper-content step="1">

											<!-- Contenido -->

											<v-row>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso1.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p><strong>Ubicar el App Store en su dispositivo.</strong></p>
													
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso2.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p>
														<strong>
															Ingresar al App Store.
														</strong>
													</p>
													
												</v-col>
											</v-row>


											<v-row class="mt-4">
												<v-col>
													<v-btn color="primary" @click="install_counter_ios = 2">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

										<v-stepper-step step="2" :complete="install_counter_ios > 2">
											Buscar la aplicación AVE Ciudad
										</v-stepper-step>

										<v-stepper-content step="2">

											<!-- Contenido -->

											<v-row>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso3.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p><strong>Presionar el botón buscar en barra de navegación inferior y ubicar la sección de búsqueda.</strong></p>
													
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso4.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p>
														<strong>
															En el campo de búsqueda superior ingresar AVE Ciudad.
														</strong>
													</p>
													
												</v-col>
											</v-row>


											<v-row class="mt-4">
												<v-col>
													<v-btn text @click="install_counter_ios = 1">Atrás</v-btn>
													<v-btn color="primary" @click="install_counter_ios = 3">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

										<v-stepper-step step="3" :complete="install_counter_ios > 3">
											Dar clic en Instalar y esperar
										</v-stepper-step>

										<v-stepper-content step="3">

											<!-- Contenido -->

											<v-row>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso5.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p><strong>Dar clic en el botón Instalar.</strong></p>
													
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso6.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p>
														<strong>
															Esperar a que la aplicación sea descargada e instalada en su dispositivo.
														</strong>
													</p>
													
												</v-col>
											</v-row>


											<v-row class="mt-4">
												<v-col>
													<v-btn text @click="install_counter_ios = 2">Atrás</v-btn>
													<v-btn color="primary" @click="install_counter_ios = 4">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

										<v-stepper-step step="4" :complete="install_counter_ios > 4">
											Ingresar a la aplicación y permitir el envio de notificaciones.
										</v-stepper-step>

										<v-stepper-content step="4">

											<!-- Contenido -->

											<v-row>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso7.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p><strong>Ubicar la aplicación AVE Ciudad en su teléfono.</strong></p>
													
												</v-col>
												<v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso8.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p>
														<strong>
															Permitir que la aplicación le envíe notificaciones.
														</strong>
													</p>
													
												</v-col>
											</v-row>


											<v-row class="mt-4">
												<v-col>
													<v-btn text @click="install_counter_ios = 3">Atrás</v-btn>
													<v-btn color="primary" @click="install_counter_ios = 5">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

										<v-stepper-step step="5" :complete="install_counter_ios > 5">
											Iniciar sesión.
										</v-stepper-step>

										<v-stepper-content step="5">

											<!-- Contenido -->

											<v-row>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso9.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p><strong>Ingresar el correo eléctronico con el cual se registro así como su contraseña y presionar INICIA SESIÓN.</strong></p>
													
												</v-col>
												<!-- <v-col cols="1" class="col-center">
													<v-icon large color="blue darken-2" class="d-none d-lg-flex d-xl-none">mdi-arrow-right-bold-circle</v-icon>
												</v-col>
												<v-col cols="12" lg="4" sm="12" md="6">
													<v-img
														src="img/ios/paso8.png"
														aspect-ratio="1"
														contain
														max-width="300"
														class="grey lighten-2"
													></v-img>
													<p>
														<strong>
															Permitir que la aplicación le envíe notificaciones.
														</strong>
													</p>
													
												</v-col> -->
											</v-row>


											<v-row class="mt-4">
												<v-col>
													<v-btn text @click="install_counter_ios = 4">Atrás</v-btn>
													<v-btn color="primary" @click="install_counter_ios = 6">
														Continuar
													</v-btn>
												</v-col>
											</v-row>
										</v-stepper-content>

									</v-stepper>

								</v-col>
							</v-row>

							<v-row class="mt-4">
								<v-col>
									<v-btn text @click="e1 = 1">
										ATRÁS
									</v-btn>
									<v-btn color="primary" @click="e1 = 3">
										Continuar
									</v-btn>
									
								</v-col>
							</v-row>
							
						</v-stepper-content>

						<!-- Paso 3 -->

						<v-stepper-content step="3">
							<v-row>
								<v-col>
									<h4>Paso 3 de 3</h4>
								</v-col>
							</v-row>

							<v-row>
								<v-col cols="12">
									<h2 class="text-center">Macro Simulacro Ciudad de Guatemala 2020</h2>
								</v-col>
								
									
								
							</v-row>

							<p style="text-align: justify;">La Coordinadora Municipal para la Reducción de Desastres a través del Plan AVE organiza y coordina el #Macro Simulacro a nivel municipal el cual se llevará a cabo el día martes 04 de febrero 2020 a las 10:00 horas.</p>

							<p>¿Para qué? </p>

							<p style="text-align: justify;">Un <strong>Simulacro</strong> es una representación de acciones de respuesta, previamente planificadas y enfocadas a un escenario específico, creado a partir de la identificación y análisis de riesgos y vulnerabilidades contenido en los planes de respuesta.</p>

							<p style="text-align: justify;">El objetivo es poner a prueba la capacidad de respuesta de la población y equipos de emergencia:</p>

							<ul style="text-align: justify;">
								<li>Evaluar y corregir una respuesta eficaz ante posibles situaciones reales de riesgo emergencia o desastre -RED-.</li>
								<li>Examinar que tan seguro es el inmueble y sus alrededores.</li>
								<li>Preparar las acciones que se llevan a cabo con base a los planes.</li>
								<li>Diseñar rutas de evacuación, así como determinar las zonas de seguridad las personas en caso de una situación de Riesgo, Emergencia o Desastre.</li>
								<li>Enlistar las herramientas y materiales que se recomienda tener a la mano para la autoprotección, comunicación y capacitación continua del personal.</li>
							</ul>

							<v-row>
								<v-col cols="12">
									<h2>Recomendaciones para el #Simulacro</h2>
								</v-col>
							</v-row>

							<h3>1.- ¿Quiénes pueden participar?</h3>

							<p style="text-align: justify;">Si nunca has participado en un Simulacro ¡Es tu oportunidad!</p>

							<p style="text-align: justify;">Toda la población puede formar parte de un Simulacro: familias, grupos voluntarios, vecinos, cuerpos de bomberos, de los sectores público y privado y medios de comunicación.</p>

							<h3>2.- ¿Cuál es el escenario o hipótesis?</h3>

							<p style="text-align: justify;">Los <strong>Simulacros</strong> deben ser planificados para un escenario que incluya la preparación de un guion con información lo más apegado a la realidad; incluyendo las acciones que debe contener el plan de respuesta.</p>

							<p style="text-align: justify;">Tu elección dependerá de <strong>los riesgos identificados de mayor probabilidad de ocurrencia</strong> en tu localidad. Por ejemplo:</p>

							<em style="text-align: justify;">Por sismo, inundación, incendio, etc.</em>

							<p class="mt-4" style="text-align: justify;">Una vez elegido el tipo de fenómeno, realizarás tu escenario conforme a: </p>

							<ul style="text-align: justify;">
								<li>Ubicación del inmueble</li>
								<li>Hora del evento</li>
								<li>Magnitud del fenómeno</li>
								<li>Tipo de fenómeno(s)</li>
								<li>Condiciones físicas del inmueble</li>
								<li>Características de operación en el inmueble</li>
								<li>Considerar además los elementos cercanos al inmueble que puedan significar una amenaza</li>
								<li>Equipamiento</li>
							</ul>

							<p style="text-align: justify;" class="mt-4">
								Para el #MacroSimulacro4f que se realizará el 04 de febrero a las 10:00 horas será hipótesis de sismo y cuyo escenario se detalla a continuación:
							</p>

							<ul style="text-align: justify;">
								<li>Tipo de sismo: Cortical</li>
								<li>Sismo de referencia: 04 de febrero de 1976 en Los Amates, Izabal</li>
								<li>Profundidad: 5 kilómetros</li>
								<li>Magnitud: 7.6</li>
							</ul>

							<h3 class="mt-4">3.- ¿Cómo me preparo antes de un #Simulacro?</h3>

							<ul style="text-align: justify;">
								<li>La planificación es la clave del éxito, para lo cual antes de realizar tu Simulacro debes tomar en cuenta la identificación de riesgos del inmueble, así como:</li>
								<li>a) Realizar un plan de evacuación / respuesta como guía</li>
								<li>b) Generar protocolos de actuación</li>
								<li>c) Simular situaciones de emergencia</li>
								<li>d) Asignar responsabilidades a cada persona</li>
								<li>e) Tener a la mano directorio telefónico, botiquín y documentos importantes</li>
								<li>f) Identificar zonas de seguridad, salidas de emergencia y puntos de reunión</li>
							</ul>

							<h3 class="mt-4">4.- Comparte en redes sociales</h3>

							<ul style="text-align: justify;">
								<li>Utiliza los HashTags #MacroSimulacro4F y #NosEstamosPreparando para difundir y mostrar las buenas prácticas y como contribuyes a la Cultura de Prevención. </li>
								<li><strong>¡No olvides qué! Un Simulacro no es un juego, de este ejercicio puede salvar tu vida o la de tu familia</strong></li>
							</ul>


							<v-row class="mt-4">
								<v-col>
									<v-btn text @click="e1 = 2">
										ATRÁS
									</v-btn>
									<!-- <v-btn color="primary" @click="e1 = 3">
										Continuar
									</v-btn> -->
									
								</v-col>
							</v-row>

						</v-stepper-content>

					</v-stepper-items>
				</v-stepper>
			</v-container>
		</v-content>
	</v-app>
</template>

<style scoped>
	.col-center {
		display: flex;
		align-items: center;
	}
</style>

<script>

export default {
	name: 'App',
	data(){
		return{
			e1: 1,
			components: [
				'Autocompletes', 'Comboboxes', 'Forms', 'Inputs', 'Overflow Buttons', 'Selects', 'Selection Controls', 'Sliders', 'Textareas', 'Text Fields',
			],
			show1: false,
			show2: false,
			os: null,
			valid: true,
			install_counter: 1,
			install_counter_ios: 1,
			registrando:false,
			usuario: {
				NOMBRE: null,
				APELLIDO: null,
				DPI: null,
				TIPO_INMUEBLE: null,
				HIPOTESIS: null,
				TIPO_INSTITUCION: null,
				NOMBRE_INSTITUCION: null,
				PERSONAL_FIJO: null,
				PERSONAL_TEMPORAL: null,
				PERSONAS_DISCAPACIDAD: null,
				ZONA: null,
				COLONIA: null,
				DIRECCION: null,
				EMAIL: null,
				TELEFONO: null,
				PASS: null,
				REPITE_PASS: null
			},
			zonas: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,21,24,25],
			tipos_inmuebles: [],
			persona: null,
			registrado: false
		}
	},
	methods: {
		registrar_usuario(){

			if(this.usuario.PASS == this.usuario.REPITE_PASS){

				if (this.$refs.form.validate()) {
					
					this.registrando = true

					console.log(this.usuario)

					this.axios({
						method: 'POST',
						url: process.env.VUE_APP_API_PERSONA,
						data: this.usuario,
						headers: {
							'Content-Type': 'application/json',
						}
					})
					.then((response) => {

						console.log(response.data)

						if (response.data.status == 'fail') {
							
							// La persona ya esta registrada mostrar notificación

							console.log(response)

							this.error_registro = response.data.message

							this.registrar_comunidad(response.data.persona)
							this.persona = response.data.persona

						}else{

							// Validar que la persona no pertenezca ya a la comunidad

							// eslint-disable-next-line no-console
							console.log(response.data);

							this.registrar_comunidad(response.data.persona[0])
							this.persona = response.data.persona[0]

						}

					})

				}else{

					Swal.fire({
						icon: 'error',
						title: 'Oops...',
						text: 'Existen campos que debe de completar!',
					})

				}

			}else{

				Swal.fire({
					icon: 'error',
					title: 'Oops...',
					text: 'La contraseña debe de coincidir!',
				})

			}

		},
		registrar_comunidad(persona){

			let data = {
				ID_PERSONA: persona.id_persona,
				ID_COMUNIDAD: process.env.VUE_APP_COMUNIDAD_ID,
				ID_ROL: process.env.VUE_APP_ROL_ID,
				ID_PERSONA_INVITO: 3941
			}

			this.axios({
				method: 'POST',
				url: process.env.VUE_APP_API_COMUNIDAD,
				data: data,
				headers: {
					'Content-Type': 'application/json',
					'api-token': process.env.VUE_APP_API_KEY
				}
			})
			.then((response) => {

				// eslint-disable-next-line no-console
				console.log(response.data)
				
				// La persona es agregada a la comunidad
				if (response.data.status == 'success') {
					
					this.registrado = false
				
					Swal.fire(
						'Excelente!',
						'El registro para el simulacro 4F ha sido exitoso!',
						'success'
					).then(()=>{
						this.e1 = 2	
					})

				}else{

					// La persona ya forma parte de la comunidad por lo que ya tiene cuenta.
					this.registrado = true

					Swal.fire(
						'Excelente',
						'Hemos detectado que ya formas parte de AVE y ya has sido agregado al MACRO SIMULACRO 4F, por favor continua con los siguientes pasos para completar tu proceso de inscripción y obtener información importante sobre el simulacro a realizarse el 4 de febrero del presente año.',
						'info'
					).then(()=>{
						this.e1 = 2
					})

					// this.persona = null

				}

				// Intentar registrar los otros datos de la persona
				this.registrar_otros_datos()

				this.usuario = {
					NOMBRE: null,
					APELLIDO: null,
					DPI: null,
					TIPO_INMUEBLE: null,
					HIPOTESIS: null,
					TIPO_INSTITUCION: null,
					NOMBRE_INSTITUCION: null,
					PERSONAL_FIJO: null,
					PERSONAL_TEMPORAL: null,
					PERSONAS_DISCAPACIDAD: null,
					ZONA: null,
					COLONIA: null,
					DIRECCION: null,
					EMAIL: null,
					TELEFONO: null,
					PASS: null,
					REPITE_PASS: null
				},

				this.$refs.form.resetValidation()

				this.registrando = false

			})

		},
		select_android(){

			console.log('android')

			this.os = 'android'
			this.install_counter = 1

			console.log(this.install_counter)
		},
		select_ios(){
			this.os = 'ios'
			this.install_counter_ios = 1
		},
		ya_registrado(){

			this.e1 = 2	

		},
		cancelar(){

			this.$refs.form.resetValidation()

		},
		registrar_otros_datos(){

			let data = {
				name: "registrar",
				param: {
					"usuario": this.usuario,
					"persona": this.persona
				}
			}

			this.axios.post(process.env.VUE_APP_API_OTROS_DATOS, data)
			.then((response) => {
				console.log(response.data)
			})

		},
		obtener_inmuebles(){

			let data = {
				name: "obtener_inmuebles",
				param: {}
			}

			this.axios.post(process.env.VUE_APP_API_OTROS_DATOS, data)
			.then((response) => {
				this.tipos_inmuebles = response.data.response.result
			})

		}	
	},
	mounted(){

		this.obtener_inmuebles()

	}
};
</script>
